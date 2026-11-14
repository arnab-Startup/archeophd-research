# Research Module 07: Radiocarbon Physics & OxCal Bayesian Mathematics

> **Component:** Chronological Calibration & OxCal Interoperability Bridge  
> **Target System:** ArchaeoPhD AI v2.0 OxCal Bridge (`engine/analysis/oxcal_compiler.hpp`)  
> **Status:** Production Reference  

---

## 1. Radiocarbon Physics & Atmospheric Non-Linearity

### 1.1 Non-Linear $^{14}\text{C}$ Production
Radiocarbon is formed in the upper atmosphere via cosmic neutron bombardment of $^{14}\text{N}$:
$$^{14}\text{N} + n \longrightarrow {}^{14}\text{C} + p$$
Because solar magnetic modulation and Earth's geomagnetic dipole field fluctuate over millennia, the atmospheric concentration of $^{14}\text{C}$ (expressed in $F^{14}\text{C}$ concentration space) varies non-linearly:
* **The Hallstatt Plateau ($\sim 750$–$400$ BCE / $\sim 2750$–$2350$ cal BP):** A 350-year flat section where natural decay roughly matches production, causing all radiocarbon samples from this era to yield nearly identical uncalibrated ages ($\sim 2450 \pm 30$ BP).

### 1.2 Cubic Spline Interpolation in $F^{14}\text{C}$ Space
OxCal performs calibration using piecewise cubic spline interpolation across discrete atmospheric calibration points (IntCal20; Reimer et al. 2020) at high resolution:
$$r(t) = r_i + a_i(t - t_i) + b_i(t - t_i)^2 + c_i(t - t_i)^3$$
Where $r(t)$ represents the calibration curve in $F^{14}\text{C}$ concentration space, and $a_i, b_i, c_i$ are spline coefficients guaranteeing continuity of $r(t)$ and its first derivative $r'(t)$.

---

## 2. Why Symmetric Intervals (Mean $\pm$ SD) Are Mathematically Invalid

When an uncalibrated Gaussian lab determination $y \pm \sigma$ is projected onto the non-monotonic calibration curve $r(t)$, the resulting calendar age likelihood function is:
$$p(t | y, \sigma) \propto \frac{\exp\left( - \frac{(y - r(t))^2}{2(\sigma^2 + \sigma_r^2(t))} \right)}{\sqrt{\sigma^2 + \sigma_r^2(t)}}$$

```
    Lab Determination (Gaussian)               IntCal20 Calibration Curve (Wiggly)
          |                                                  / \
          |                                                 /   \       /--- Plateau
          v                                                /     \_____/
     +---------+                                          /
     | y +/- s | --------------------------------------->+
     +---------+                                          \         / \
                                                           \_______/   \
                                                                        v
                                                          Calibrated Calendar Likelihood
                                                          (Multimodal / Asymmetric)
                                                                _/\_      __/\_
                                                          -----+----+----+-----+----
                                                               Sub-1     Sub-2
```

* **Conclusion:** Projecting a single Gaussian measurement across a non-monotonic curve yields a **multimodal, highly asymmetric posterior distribution**.
* Reporting a calibrated date as a symmetric Mean $\pm$ SD interval (e.g., $1250 \pm 45$ cal BCE) assumes a normal bell curve, which is mathematically false and rejected by professional archaeological journals (*Radiocarbon*, *Journal of Archaeological Science*).
* Dates must be reported as **95.4% (2$\sigma$) Highest Posterior Density (HPD) disjoint sub-intervals**.

---

## 3. Marine and Freshwater Reservoir Offsets ($\Delta R$)

When organisms consume carbon from reservoirs depleted of $^{14}\text{C}$ (oceans, limestone-rich freshwater bodies), an offset $\Delta R = r_d \pm s_d$ must be incorporated:
$$p(y_i | t_i, r_d) \propto \frac{\exp\left[-\frac{(y_i - r(t_i) - r_d)^2}{2(s_i^2 + s^2(t_i) + s_d^2)}\right]}{\sqrt{s_i^2 + s^2(t_i) + s_d^2}}$$

---

## 4. OxCal Bayesian Agreement Indices

OxCal validates stratigraphic prior constraints against radiocarbon likelihoods using Agreement Indices ($A$):
* **Individual Agreement Index ($A_i$):**
  $$A_i = 100 \times \frac{\int p_{\text{posterior}}(t) \, p_{\text{likelihood}}(t) \, dt}{\int [p_{\text{likelihood}}(t)]^2 \, dt}$$
* **Model Agreement Index ($A_{\text{model}}$):**
  $$A_{\text{model}} = 100 \times (F_{\text{model}})^{1/\sqrt{n}}$$
* **Threshold:** If $A_i < 60\%$ or $A_{\text{model}} < 60\%$, there is statistically significant conflict between the prior stratigraphic sequence and the radiocarbon determination at the $\alpha = 0.05$ level.
* **MCMC Convergence ($C$):** Convergence across all Markov chains must satisfy $C \ge 95\%$.

---

## 5. Headless OxCal Bridge & CQL2 Compilation

ArchaeoPhD AI v2.0 auto-compiles extracted text and stratigraphic relationships into verifiable **Chronological Query Language 2 (CQL2)**:

```cql2
Plot()
{
  Curve("IntCal20","intcal20.14c");
  Sequence("Stratum 4aLH Sequence")
  {
    Boundary("Start");
    Phase("Intra-Stratum Dates")
    {
      R_Date("OxA-30638", 28000, 220)
      {
        Outlier_Model("SSimple", N(0,2), 0, "s");
      };
      R_Date("OxA-30639", 27400, 200);
    };
    Boundary("End");
  };
};
```

The system executes the local headless OxCal binary via CLI subprocess, intercepts the output files, and parses the multimodal 95.4% HPD intervals and $A_i$ diagnostics into the knowledge base.

# EP01 — Can AI Really Understand Physics?

**Hyper Technology — Physics-Informed Machine Learning (PIML)**  
**Unit 01 — The Big Picture · Conceptual computation companion**

## What you will learn

Matching observed data does not guarantee that a field satisfies a governing physical law. This beginner-friendly lab makes that distinction visible using a cooling rod, five synthetic sensors, and a controlled counterexample. It is an introductory experiment, with no neural-network training. The first full PINN training lesson is Episode 11 in the approved curriculum.

## Open and run in Google Colab

1. Download `EP01_Heat_Equation_Conceptual_Lab.ipynb` from this folder.
2. Open [Google Colab](https://colab.research.google.com/), choose **File → Upload notebook**, and select the file.
3. Use a **Python 3 CPU** runtime. No GPU, dataset upload, package installation, or manual input is needed.
4. Select **Runtime → Run all**. Read the explanations and actual plots in order.
5. The final verification cell should list **29 PASS** results. Running the notebook creates `figures/`, `data/`, and `verification_report.json` relative to the current notebook working directory.

Only NumPy and Matplotlib are required beyond Python's standard library. The notebook records the runtime's actual versions. The delivered version was tested with Python 3.12.14, NumPy 2.5.2, and Matplotlib 3.11.1. Colab's installed versions can differ.

**Execution disclosure:** all 13 code cells were run in order in a fresh local Python process with a fresh IPython namespace, with genuine outputs saved. Hosted execution inside Google Colab has not been independently verified by the production agent. The course creator has separately confirmed a successful Run all in Google Colab. The recorded fresh local execution evidence remains in `execution_status.json` and `VERIFICATION_REPORT.md`.

## Physical benchmark

The rod has length $L=0.10\,\mathrm m$ and constant thermal diffusivity $\alpha=10^{-4}\,\mathrm{m^2/s}$. For $0\le t\le20\,\mathrm s$,

$$\partial_t T=\alpha\partial_{xx}T,\qquad T(0,t)=T(L,t)=20^\circ\mathrm C,$$

$$T(x,0)=20+60\sin(\pi x/L),$$

$$T_{\mathrm{exact}}(x,t)=20+60\sin(\pi x/L)\exp(-\alpha\pi^2t/L^2).$$

Assumptions: homogeneous one-dimensional conduction, constant material properties and diffusivity, no internal heat source, insulated lateral surfaces, and temperature-controlled ends that exchange heat with reservoirs. The initial temperature is spatially varying; only the midpoint initially reaches 80 °C. The midpoint is approximately 28.3347 °C at 20 s, and approaches 20 °C as time continues.

## Synthetic observations and counterexample

The five interior virtual sensors are $x_k=kL/6$, for $k=1,\ldots,5$. Their observations are noiseless values computed from the analytical reference, not laboratory measurements.

$$T_c=T_{\mathrm{exact}}+A\sin(6\pi x/L)(1-e^{-t/\tau_c}),\qquad A=10^\circ\mathrm C,\quad\tau_c=5\,\mathrm s.$$

This is an **analytically constructed counterexample**, not a neural-network prediction, trained PINN, or optimized field. It matches all five sensors for every time mathematically, and preserves the initial and boundary conditions. It generally violates the Heat Equation elsewhere. Its PDE residual also vanishes at the sensor positions: checking only those locations can miss the failure.

With $q=6\pi/L$, its residual is

$$r=\partial_tT_c-\alpha\partial_{xx}T_c
=A\sin(qx)\left[\frac{e^{-t/\tau_c}}{\tau_c}+\alpha q^2(1-e^{-t/\tau_c})\right].$$

Temperature differences have units °C; residuals have units °C/s. Sensor agreement is not physics-loss minimization. This experiment does not establish the accuracy, speed, or superiority of any trained model. It does not contradict uniqueness of the correctly posed heat problem, because the candidate fails its PDE. Finite sampled checks alone are not a universal proof of correctness.

## Relation to the episode

The established heat benchmark is preserved. This notebook extends the idea with five **interior** sensor time series and an explicit time-dependent counterexample. It does not claim to reproduce the video's particular five-position illustration or any genuine trained-model experiment. No episode video or ManimGL source was modified.

## Included outputs

- One executed, self-contained notebook with learning objectives, derivations, numerical verification, interpretation, and student exercises.
- Seven computed PNG figures, each **3840 × 2160**: temperature snapshots, exact space–time field, five synthetic sensors, reference versus candidate, signed temperature difference, candidate PDE residual, and sensor/off-sensor comparisons.
- `data/EP01_heat_equation_verified_arrays.npz`: compact numerical arrays for scientific visualization in ManimGL. Load with `numpy.load(path, allow_pickle=False)`.
- `verification_report.json`, `VERIFICATION_REPORT.md`, and `execution_status.json`.

The main exported fields have orientation `[time_index, position_index]`. Positions are in m, times in s, temperatures/differences in °C, and residuals in °C/s. The archive includes metadata and parameter values.

### Array inventory

| Name | Shape | Data type |
|---|---|---|
| `x_m` | `(1201,)` | `float64` |
| `t_s` | `(201,)` | `float64` |
| `exact_C` | `(201, 1201)` | `float64` |
| `candidate_C` | `(201, 1201)` | `float64` |
| `error_C` | `(201, 1201)` | `float64` |
| `candidate_residual_C_per_s` | `(201, 1201)` | `float64` |
| `sensor_x_m` | `(5,)` | `float64` |
| `sensor_reference_C` | `(201, 5)` | `float64` |
| `sensor_candidate_C` | `(201, 5)` | `float64` |
| `selected_times_s` | `(4,)` | `float64` |
| `snapshot_s` | `()` | `float64` |
| `sensor_snapshot_C` | `(5,)` | `float64` |
| `off_sensor_x_m` | `()` | `float64` |
| `sensor_error_series_C` | `(201,)` | `float64` |
| `off_error_series_C` | `(201,)` | `float64` |
| `sensor_residual_series_C_per_s` | `(201,)` | `float64` |
| `off_residual_series_C_per_s` | `(201,)` | `float64` |
| `metadata_json` | `()` | `<U440` |

## Expected verification

All 29 assertions should pass, covering initial and boundary conditions, sensor agreement, exact-solution PDE cancellation, independently calculated finite differences and convergence, residual signs and units interpretation, off-sensor failure, and exported-array consistency. Small differences near machine precision are expected. The numerical finite-difference check refines toward zero for the exact solution and toward the derived nonzero residual for the candidate.

## References and publication

- Karniadakis et al. (2021), [Physics-informed machine learning](https://doi.org/10.1038/s42254-021-00314-5), Nature Reviews Physics 3, 422–440.
- Raissi, Perdikaris and Karniadakis, [Physics-informed neural networks — author project](https://maziarraissi.github.io/PINNs/).
- [Google Colab FAQ](https://research.google.com/colaboratory/faq.html).
- Hyper Technology, approved 70-Episode Master Curriculum v1.1 (2026), EP01 scope and EP11 training placement.

## Episode Video

Watch the course on the [official Hyper Technology YouTube channel](https://www.youtube.com/@hypertechnology4273). The direct EP01 video link will be added after the episode is published.

[Official course repository](https://github.com/Mo88maher/Hyper-Technology-PIML-Course) · [Course index](../../README.md)

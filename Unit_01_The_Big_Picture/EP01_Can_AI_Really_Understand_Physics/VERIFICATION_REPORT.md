# EP01 — Verification and execution report

## Result

**29/29 notebook assertions PASS. All 13 code cells executed in order with zero errors.** Actual computed notebook outputs are saved in the delivered `.ipynb`. Seven computed 4K figures were exported and visually inspected, including a corrected final comparison layout.

## Execution evidence and scope

The final run used a fresh local Python process with a fresh IPython namespace and took 7.64 seconds. Matplotlib used a noninteractive backend and captured inline display output. This tests sequential code execution without pre-existing notebook variables; it is not a claimed hosted Colab or Jupyter-kernel-protocol execution. **Google Colab itself has not been independently tested.** The notebook uses CPU, NumPy, Matplotlib and standard-library modules, relative paths, generated data, and no manual inputs or installation cells.

Tested versions: Python 3.12.14; NumPy 2.5.2; Matplotlib 3.11.1. The notebook records versions again on each run. Machine-readable evidence is in `verification_report.json` and `execution_status.json`.

## Mathematical verification

The reference solves the homogeneous constant-diffusivity heat equation: the spatial second derivative of its sine mode multiplies it by −(π/L)², exactly matching its time derivative after multiplication by α. The initial exponential is one; the sine vanishes at the endpoints.

For the added disturbance, q = 6π/L and g(t) = 1 − exp(−t/τc). Its time derivative is A sin(qx) exp(−t/τc)/τc, and its second spatial derivative is −A q² sin(qx) g(t). Subtracting α times that derivative gives a **positive** second contribution to the residual. Both bracketed terms have units 1/s, giving residual units °C/s. The temperature difference retains units °C.

At sensor k, sin(q xk) = sin(kπ) = 0, so both disturbance and residual vanish there analytically. At t = 0 the disturbance vanishes but its time derivative generally does not: matching an initial state does not imply satisfying its evolution equation. The independent SymPy 1.14.0 audit confirmed reference PDE cancellation, candidate residual, sensor zeros, initial and boundary conditions. SymPy is not a notebook dependency.

## Actual numerical results

| Metric (units in name) | Value |
|---|---:|
| max_sensor_difference_C | 2.48689957516e-14 |
| max_field_difference_C_on_export_grid | 9.81684361111 |
| max_candidate_residual_C_per_s_on_export_grid | 34.916441925 |
| max_exact_analytic_residual_C_per_s | 1.7763568394e-15 |
| midpoint_temperature_at_20s_C | 28.3346679886 |
| off_sensor_at_L_over_12_t5s_difference_C | 6.32120558829 |
| off_sensor_at_L_over_12_t5s_residual_C_per_s | 23.1953663403 |

Domain maxima are sampled-grid maxima, not asserted continuous optimization results. The grid has 201 times and 1201 positions. Sensor agreement is at floating-point tolerance; the analytical identity holds for all times.

### Independent centered finite differences

| Δx (m) | Δt (s) | Exact field max numerical residual (°C/s) | Max discrepancy from derived candidate residual (°C/s) |
|---:|---:|---:|---:|
| 0.00025 | 0.02 | 3.30562038e-05 | 0.0064446297 |
| 0.000125 | 0.01 | 8.26406321e-06 | 0.00161124693 |
| 0.0000625 | 0.005 | 2.06625543e-06 | 0.000402817393 |

Candidate discrepancy refinement ratios are 3.99977779 and 3.99994380, consistent with second-order convergence under joint step halving on the test grid.

## Checks

- `exact_initial_condition`: **PASS**
- `candidate_initial_condition`: **PASS**
- `exact_left_boundary`: **PASS**
- `exact_right_boundary`: **PASS**
- `candidate_left_boundary`: **PASS**
- `candidate_right_boundary`: **PASS**
- `sensor_positions_strictly_interior`: **PASS**
- `five_sensor_time_series_agree`: **PASS**
- `exact_reference_symmetry`: **PASS**
- `exact_reference_temperature_bounds`: **PASS**
- `midpoint_still_above_boundary_at_20s`: **PASS**
- `exact_analytical_pde_cancellation`: **PASS**
- `candidate_residual_independent_finite_differences`: **PASS**
- `candidate_residual_second_order_convergence`: **PASS**
- `exact_residual_independent_finite_differences`: **PASS**
- `exact_residual_refines_toward_zero`: **PASS**
- `candidate_nonzero_off_sensor_residual`: **PASS**
- `candidate_residual_sign_at_positive_sine`: **PASS**
- `candidate_residual_sign_at_negative_sine`: **PASS**
- `candidate_residual_zero_at_sensors`: **PASS**
- `initial_disturbance_zero_but_rate_nonzero`: **PASS**
- `export_exact_array_consistency`: **PASS**
- `export_candidate_array_consistency`: **PASS**
- `export_error_array_consistency`: **PASS**
- `export_residual_array_consistency`: **PASS**
- `export_sensor_array_consistency`: **PASS**
- `export_snapshot_array_consistency`: **PASS**
- `export_comparison_series_consistency`: **PASS**
- `seven_figure_exports_exist`: **PASS**

## Figure evidence

- `figures/01_temperature_snapshots_4K.png` — 3840 × 2160. Analytical temperature profiles at 0, 5, 10, and 20 seconds.
- `figures/02_exact_spacetime_field_4K.png` — 3840 × 2160. The analytical field; every pixel uses the time-by-position temperature array.
- `figures/03_five_synthetic_sensors_4K.png` — 3840 × 2160. Five interior sensor positions and their computed reference readings at 5 seconds.
- `figures/04_reference_vs_counterexample_4K.png` — 3840 × 2160. Both fields agree at the five synthetic observations but differ between them at 5 seconds.
- `figures/05_signed_field_difference_4K.png` — 3840 × 2160. Signed difference uses ERROR_C; dotted sensor lines coincide with zero disturbance.
- `figures/06_candidate_pde_residual_4K.png` — 3840 × 2160. Signed residual calculated from the derived expression; zero sensor residual hides off-sensor failure.
- `figures/07_sensor_vs_off_sensor_checks_4K.png` — 3840 × 2160. Separate panels compare temperature differences and PDE residuals at a sensor and an off-sensor point.

Exported arrays are checked against independently recomputed field values. The plotting cells use these computed fields and clearly distinguish synthetic observations, reference values and the constructed candidate. The error and residual have different physical units and separate scales. Figure dimensions and notebook output integrity were checked again during packaging.

## Limits and preservation

This is a conceptual analytical experiment, with no learned model, physics-based loss optimization, or training result. Physical assumptions and model validity remain essential. Tests on finite grids cannot certify arbitrary candidate functions everywhere. The notebook preserves the established heat benchmark but extends the video's illustrative sensor setup; it does not claim to reproduce a trained-model comparison. Full PINN training remains assigned to Episode 11.

No existing video, ManimGL source, GitHub content, repository visibility, or approved production assets were modified. The private repository's remote contents were not accessible for inspection. The delivered tree is ready for later GitHub publication; no push and no video notebook preview were produced.

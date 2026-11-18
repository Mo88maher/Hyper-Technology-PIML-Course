# Hyper Technology — Physics-Informed Machine Learning Course

Official Hyper Technology course on Physics-Informed Machine Learning, including scientific Python notebooks, PINNs, simulations, and reproducible experiments.

**70 planned episodes · 13 units · 3 stages.** Materials are released progressively after review. The EP01 verified conceptual companion is included; the remaining lesson folders are a curriculum roadmap, not completed experiments.

[Watch Hyper Technology on YouTube](https://www.youtube.com/@hypertechnology4273) · [Full curriculum](CURRICULUM.md) · [EP01 notebook](Unit_01_The_Big_Picture/EP01_Can_AI_Really_Understand_Physics/EP01_Heat_Equation_Conceptual_Lab.ipynb) · [EP01 guide](Unit_01_The_Big_Picture/EP01_Can_AI_Really_Understand_Physics/README.md)

## Learning sequence

1. **Foundations — EP01–EP10:** scientific problem formulation, differential equations, conservation, boundary conditions, numerical solvers, neural networks and automatic differentiation.
2. **PINNs — EP11–EP42:** construction, validation, failure modes, optimization, PDE examples, inverse problems, uncertainty and advanced formulations.
3. **Broader SciML and research — EP43–EP70:** equation discovery, dynamical systems, geometry, operator learning, hybrid and differentiable physics, and research projects.

## Course units

| Unit | Episodes | Count | Topic |
|---|---|---:|---|
| 01 | EP01–EP03 | 3 | [The Big Picture](Unit_01_The_Big_Picture/README.md) |
| 02 | EP04–EP10 | 7 | [Mathematical & ML Foundations](Unit_02_Mathematical_and_ML_Foundations/README.md) |
| 03 | EP11–EP17 | 7 | [Your First PINNs](Unit_03_Your_First_PINNs/README.md) |
| 04 | EP18–EP26 | 9 | [Why PINNs Fail & How to Fix Them](Unit_04_Why_PINNs_Fail_and_How_to_Fix_Them/README.md) |
| 05 | EP27–EP33 | 7 | [The PDE Zoo](Unit_05_The_PDE_Zoo/README.md) |
| 06 | EP34–EP39 | 6 | [Inverse Problems, Data & Uncertainty](Unit_06_Inverse_Problems_Data_and_Uncertainty/README.md) |
| 07 | EP40–EP42 | 3 | [Advanced PINN Formulations](Unit_07_Advanced_PINN_Formulations/README.md) |
| 08 | EP43–EP45 | 3 | [Equation Discovery](Unit_08_Equation_Discovery/README.md) |
| 09 | EP46–EP50 | 5 | [Dynamical Systems & Structure-Preserving Learning](Unit_09_Dynamical_Systems_and_Structure_Preserving_Learning/README.md) |
| 10 | EP51–EP53 | 3 | [Symmetry, Geometry & Graphs](Unit_10_Symmetry_Geometry_and_Graphs/README.md) |
| 11 | EP54–EP59 | 6 | [Operator Learning & Foundation Models](Unit_11_Operator_Learning_and_Foundation_Models/README.md) |
| 12 | EP60–EP64 | 5 | [Reduced-Order, Hybrid & Differentiable Physics](Unit_12_Reduced_Order_Hybrid_and_Differentiable_Physics/README.md) |
| 13 | EP65–EP70 | 6 | [Applications, Benchmarking & Research](Unit_13_Applications_Benchmarking_and_Research/README.md) |

## Start with Episode 01

The [EP01 companion](Unit_01_The_Big_Picture/EP01_Can_AI_Really_Understand_Physics/README.md) is an executed, self-contained conceptual heat-equation lab. It includes 29 passing verification checks, seven computed figures and the exported numerical arrays. It uses CPU, NumPy and Matplotlib. It illustrates why matching sensor readings is different from satisfying a physical law; it does not train a neural network. The first full PINN training lesson in this curriculum is EP11.

Download the notebook and upload it to [Google Colab](https://colab.research.google.com/), then use **Runtime → Run all**. The episode guide explains the expected results and execution evidence.

## Repository layout

Each unit has an index. Each episode has its own folder and README. Verified lesson folders contain the notebook, run evidence, figures and any required data. Planned lesson folders contain an explicit status and their approved title. Videos are hosted on the Hyper Technology YouTube channel.

## Scientific scope

This course distinguishes SciML, PIML and PINNs, identifies how physical knowledge enters a method, and separates conceptual illustrations from actual trained-model results. Experiments are reviewed lesson by lesson; inclusion in the roadmap does not imply that a future experiment has already been executed.

Curriculum source: Hyper Technology, Master Curriculum v1.1, 70 episodes and 13 units, approved November 2026.

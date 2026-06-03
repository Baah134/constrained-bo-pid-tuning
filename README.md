# Constraint-Aware Bayesian Optimization for PID Tuning

Code and results for the paper:

> **Constraint-Aware Bayesian Optimization for PID Tuning: Discovering
> Plant-Specific Control Strategies**
> Prince Baah-Mensah, Stephen K. Armah
> Automation, Robotics and Controls Lab, Ashesi University
> *Submitted to IEEE CCTA 2026*

## Overview

This repository contains the full experimental pipeline comparing
constraint-aware Bayesian Optimization (BO) against MATLAB's `pidtune`
for PID controller tuning across four linear SISO plants.

The central argument of the paper is that framing PID tuning as a
**constrained optimization problem** — rather than a
bandwidth-maximization heuristic — produces controllers that satisfy
engineering specifications by design, and discovers qualitatively
different control strategies tailored to each plant's dynamics.

## Key Results

| Plant | MATLAB settling (s) | BO settling (s) | MATLAB OS (%) | BO OS (%) |
|---|---|---|---|---|
| Mass-spring-damper | 1.242 | **0.127** | 6.71 | **1.16** |
| 3rd-order (P1) | 3.169 | **2.654** | 5.30 | **1.15** |
| Non-min phase (P2) | 7.712 | **5.576** | **0.72** | 1.95 |
| Resonant (P3) | 2.283 | **0.067** | 14.97 | **5.17** |

Under ±20% plant parameter perturbation, BO controllers maintain
overshoot-spec compliance in **94% of cases** vs. **22%** for
MATLAB's `pidtune`.


## Plants Studied

| Label | Transfer Function | Challenge |
|---|---|---|
| MSD | $1/(s^2+10s+20)$ | Benchmark, in-depth analysis |
| P1 | $1/[(s+1)(s+2)(s+3)]$ | Higher-order dynamics |
| P2 | $(1-0.5s)/[(s+1)^2(s+2)]$ | Right-half-plane zero |
| P3 | $(s+3)/[(s+1)(s^2+0.4s+4)]$ | Lightly damped resonance |

## Dependencies

- Python 3.9+
- `python-control` >= 0.9.4
- `optuna` >= 3.0.0
- `numpy`, `scipy`, `matplotlib`, `pandas`

Full list in `requirements.txt`.


*Update with DOI and page numbers after publication.*

## License

MIT License. See `LICENSE` for details.

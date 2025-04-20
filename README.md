# Reinforcement Learning for Critical Hypotension Treatment

This repository explores the application of offline reinforcement learning (RL) methods for optimizing treatment strategies in ICU patients suffering from acute hypotension. Leveraging synthetic data generated from the MIMIC-III dataset, we evaluate both model-free and model-based approaches for personalized, data-driven decision support in critical care.

## Objective

To develop RL-based agents capable of recommending safe and effective treatment strategies—specifically, fluid boluses and vasopressors—based on vital signs and other clinical indicators, aiming to improve outcomes in hypotensive patients.

## Repository Structure

- `Model Based Preprocessing.ipynb`: Prepares the dataset for the model-based Dyna-Q approach, including state discretization and transition modeling.
- `Model Based.ipynb`: Implements the Dyna-Q algorithm using KNN-based transition approximation and explores SOFA-based reward structures.
- `Model Free.ipynb`: Implements and evaluates several offline RL algorithms, including:
  - Tabular Q-Learning
  - Batch Constrained Q-Learning (BCQ)
  - Conservative Q-Learning (CQL)
  - Distributional Deep Q-Networks (DQN)

## Models and Methods

- **Tabular Q-Learning**: Serves as a baseline using clustered states and observed transitions.
- **BCQ**: Constrains actions to observed clinician decisions to ensure safety.
- **CQL**: Penalizes overestimation of unobserved actions, prioritizing conservatism.
- **Distributional DQN**: Models return distributions for better uncertainty handling.
- **Dyna-Q**: A model-based method combining real and simulated experience using approximate transition dynamics.

## Dataset

- **Source**: Health Gym’s synthetic ICU dataset based on MIMIC-III.
- **Scope**: 3,910 patients, 48-hour time-series data, 22 variables.
- **Action Space**: 16 discrete combinations of fluid and vasopressor interventions.

## Reward Functions

1. **MAP-Based Reward**: Encourages maintaining adequate blood pressure and urine output.
2. **SOFA-Based Reward**: Evaluates the impact of integrating organ failure metrics on policy effectiveness.

## Evaluation

Models were evaluated using:
- **Weighted Importance Sampling (WIS)** for off-policy evaluation.
- **Action Agreement Metrics** to compare model recommendations against clinician behavior.
- **Cumulative Rewards** to assess policy effectiveness.

### Key Results

| Policy              | Expected Cumulative Reward |
|---------------------|----------------------------|
| Clinician Policy    | -2.224                     |
| Tabular Q-Learning  | -0.247                     |
| BCQ Policy          | **-0.148**                 |
| CQL Policy          | -1.864                     |
| Distributional DQN  | -0.206                     |
| Dyna-Q              | -1.230                     |

BCQ and Distributional DQN achieved the best performance, balancing effectiveness and clinical alignment. Dyna-Q underperformed due to challenges in transition modeling.

## Limitations

- Transition dynamics in model-based RL are hard to estimate.
- Reward design remains a critical challenge.
- Dataset lacks demographics and comorbidities, limiting realism.
- Interpretability and clinician trust are key hurdles to deployment.

## References

This work builds on prior research in offline RL in healthcare, including:
- Komorowski et al. (2018)
- Fujimoto et al. (2018)
- Kumar et al. (2020)


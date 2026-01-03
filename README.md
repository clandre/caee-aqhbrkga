# AHBRKA Optimizer

This project contains optimization experiments based on Learning-based Hybrid Genetic Algorithm Approach for Hyperparameter Optimization paper.

The precompiled executable are located at:

dist/ahbrka and dist/ahbrkga_rl

---

## Expected project structure

For each dataset, the following directory structure is required:

datasets/
  <DATASET>/
    train.csv
    test.csv
    <experiment_number>.yml

During execution, a log file is automatically created or updated at:

datasets/<DATASET>/<experiment_number>.log

---

## How to run

The `--dataset` argument is mandatory.

### Minimal example

```bash
./dist/ahbrka --dataset Cosmos --experiment_number 0
```

### Command-line arguments

| Argument               |   Type |      Default | Description                                                                            |
| ---------------------- | -----: | -----------: | -------------------------------------------------------------------------------------- |
| `--dataset`            | string | *(required)* | Dataset name (folder inside `datasets/`).                                              |
| `--experiment_number`  |    int |          `1` | Selects the experiment and the YAML file `datasets/<DATASET>/<experiment_number>.yml`. |
| `--percentage`         |  float |        `0.7` | Percentage parameter passed to the decoder / exploitation methods.                     |
| `--epochs_no`          |    int |        `300` | Number of training epochs used by the neural model.                                    |
| `--batch_size`         |    int |      `30000` | Batch size.                                                                            |
| `--generations_no`     |    int |         `10` | Maximum number of BRKGA generations (genetic mode).                                    |
| `--genetic_experiment` |   flag |      `false` | Enables BRKGA evolutionary mode.                                                       |
| `--reinforcement`      |   flag |      `false` | Enables reinforcement-based selection (if implemented/configured).                     |
| `--ml_step`            | choice |      `train` | ML stage: `train` or `eval` (currently not used directly in the main flow).            |

## Experiment numbering and definitions

The behavior of the executable depends on the value of `--experiment_number` and on whether the `--reinforcement` flag is enabled.

The experiments are identified according to the following mapping:

| Experiment Number | Experiment Name |
|-------------------|-----------------|
| 0 | Random Search |
| 1 | Grid Search |
| 2 | Bayesian Optimization |
| 3 | CMA-ES |
| 4 | BRKGA |
| 5 | BRKGA + CMA-ES |
| 6 | HBRKGA-BW |
| 7 | HBRKGA-BW + CMA-ES |
| 8 | HBRKGA-RW |
| 9 | HBRKGA-RW + CMA-ES |
| 10 | A-HBRKGA |
| 11 | A-HBRKGA + CMA-ES |

---

## Reinforcement-based experiments (`--reinforcement`)

When the flag `--reinforcement` is set to `true`, experiments **10** and **11** have a specific meaning and are interpreted as **Q-learning–based HBRKGA variants**:

| Experiment Number | Reinforcement-based Interpretation |
|-------------------|-----------------------------------|
| 10 | **Q-HBRKGA – CMA-ES** |
| 11 | **Q-HBRKGA** |

In this case, reinforcement learning is used to guide the selection of exploitation strategies during the evolutionary process.

---

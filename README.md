# PROMIS: Reinforcement Learning-Driven Prompt Optimization for Code Generation

PROMIS explores prompt optimization for code generation using reinforcement learning and lexical and semantic prompt transformations. Rather than relying on a single prompt-rewriting strategy, the system uses Proximal Policy Optimization (PPO) to select an action based on feedback from generated code.

The implementation was developed for experiments on the Mostly Basic Python Problems (MBPP) benchmark. It includes experiments with CodeT5+ and CodeLlama as code generation models, LLaMA-based prompt rewriting, an evolutionary text-mutation strategy based on EPiC, and feedback inspired by Reflexion.

## Approach

For each programming problem, the system starts with the task description and considers several ways to modify the prompt. The available strategies include keeping the original prompt, lexical mutations, and semantic rewriting. Candidate prompts are passed to a code generation model, and generated Python code is evaluated against the available tests. The resulting feedback informs the PPO policy for subsequent action selection.

The main components are:

- **RLPromptEnv:** Gymnasium environment for prompt optimization and reward calculation.
- **PPOAgent:** policy trained to select prompt-modification actions.
- **PromptRewriter:** LLaMA-based semantic rewriting.
- **Epic_GA:** lexical and evolutionary mutations informed by the [EPiC approach](https://github.com/HamedTaherkhani/EPiC).
- **Feedback and evaluation:** execution of generated code against tests, with additional feedback mechanisms inspired by [Reflexion](https://github.com/noahshinn/reflexion).

The models described in the original experiments are `Salesforce/codet5p-770m-py`, `CodeLlama-7b-Instruct`, and `Llama-3.2-3B-Instruct` for rewriting. See the configuration and experiment files for model-specific settings.

## Repository layout

| Path | Contents |
| --- | --- |
| `ppo_codet5/` | Python package for the training and evaluation pipeline |
| `ppo_codet5/agents/` | PPO agent implementation |
| `ppo_codet5/environments/` | Prompt optimization environment |
| `ppo_codet5/models/` | Code generation and prompt transformation components |
| `examples/` | Example scripts |
| `docs/` | Additional documentation |
| `sample Results/` | Sample experiment outputs |

## Installation

The package declares support for Python 3.8 and later. A CUDA-capable GPU is recommended for the larger model experiments; memory needs depend on the model and training configuration.

Clone this repository and install the dependencies:

```bash
git clone https://github.com/alimohammadiesfahani/PROMIS.git
cd PROMIS
python -m pip install -r requirements.txt
python -m pip install -e .
```

Some NLP components may need additional NLTK resources:

```python
import nltk

nltk.download("wordnet")
nltk.download("averaged_perceptron_tagger")
nltk.download("stopwords")
```

## Running the experiments

The project exposes a `ppo-codet5` command-line interface. For example:

```bash
ppo-codet5 config --output config.json
ppo-codet5 train --config config.json --output-dir ./results
ppo-codet5 eval --checkpoint ./results/final_model.pt --episodes 50
```

The generated configuration controls the code generation model, training parameters, dataset settings, and evaluation behavior. Review the configuration before running an experiment, especially on a machine with limited GPU memory.

The repository also provides Python examples in `examples/` and implementation details under `ppo_codet5/`.

## Dataset and evaluation

Experiments use the [MBPP benchmark](https://github.com/google-research/google-research/tree/master/mbpp), which contains short Python programming tasks and associated tests. The original project documentation describes experiments using 374 training examples and a collection of 974 problems.

Two metrics are reported in the original results table: Pass@1 and SoftPass@1. Pass@1 measures whether a generated solution passes the evaluation tests on the first attempt. SoftPass@1 is also reported by the project; consult the evaluation implementation for its precise definition before comparing it with results from other repositories.

## Reported results

The following values are reproduced from the original project README. They are included as project-reported experimental results, not as independently reproduced benchmark measurements.

| Strategy | CodeT5+ Pass@1 | CodeT5+ SoftPass@1 | CodeLlama Pass@1 | CodeLlama SoftPass@1 |
| --- | ---: | ---: | ---: | ---: |
| Direct generation | 12.84% | 22.80% | 41.91% | 48.82% |
| Genetic mutation | 20.23% | 33.40% | 43.01% | 51.70% |
| Semantic rewriting | 23.73% | 36.90% | 46.20% | 55.20% |
| Randomized selection (10 steps) | 31.12% | 44.10% | 49.08% | 58.60% |
| EPiC | 41.89% | 54.20% | 51.40% | 61.50% |
| Reflexion | 41.63% | 55.10% | 52.70% | 63.60% |
| PPO agent (PROMIS) | 57.58% | 67.90% | 64.80% | 73.10% |

These results suggest that learning which prompt-modification strategy to apply can be more effective than using a fixed strategy in the reported setup. Comparisons with other published implementations depend on matching dataset splits, generation settings, test execution rules, and evaluation budgets.

## Related work and acknowledgments

The project draws on ideas and components from the following work:

- [EPiC: Evolutionary Prompt Engineering for Code Generation](https://github.com/HamedTaherkhani/EPiC)
- [Reflexion: Language Agents with Verbal Reinforcement Learning](https://github.com/noahshinn/reflexion)
- [CodeT5+](https://huggingface.co/Salesforce/codet5p-770m-py)
- [Code Llama](https://github.com/facebookresearch/codellama)
- [MBPP benchmark](https://github.com/google-research/google-research/tree/master/mbpp)

Please refer to the associated conference paper for the full experimental methodology and scholarly citations.


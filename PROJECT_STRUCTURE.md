# PPO-CodeT5 Project Structure

## Directory Structure

```
Alicode/
├── ppo_codet5/                    # Main package
│   ├── __init__.py               # Package initialization
│   ├── config.py                 # Configuration management
│   ├── main.py                   # Main training/evaluation logic
│   ├── cli.py                    # Command line interface
│   ├── agents/                   # RL agents
│   │   ├── __init__.py
│   │   └── ppo_agent.py          # PPO agent implementation
│   ├── environments/             # RL environments
│   │   ├── __init__.py
│   │   └── rl_prompt_env.py      # Prompt optimization environment
│   ├── models/                   # ML models
│   │   ├── __init__.py
│   │   ├── prompt_rewriter.py    # LLaMA-based prompt rewriter
│   │   ├── genetic_algorithm.py  # Text mutation GA
│   │   └── codet5_model.py       # CodeT5+ wrapper
│   ├── utils/                    # Utility modules
│   │   ├── __init__.py
│   │   ├── logging.py            # Logging utilities
│   │   ├── text_processing.py    # Text processing utilities
│   │   ├── evaluation.py         # Code evaluation utilities
│   │   └── file_utils.py         # File I/O utilities
│   └── data/                     # Data processing modules
├── examples/                     # Example scripts
│   ├── basic_training.py         # Basic training example
│   ├── custom_config.py          # Custom configuration example
│   └── evaluation_example.py     # Evaluation example
├── tests/                        # Test modules
├── docs/                         # Documentation
├── 01_ppo_codet5.ipynb          # Original Jupyter notebook
├── README.md                     # Main documentation
├── CONTRIBUTING.md               # Contribution guidelines
├── LICENSE                       # MIT License
├── requirements.txt              # Python dependencies
├── setup.py                      # Package setup
├── install.sh                    # Linux/Mac installation script
└── install.bat                   # Windows installation script
```

## Architecture Overview

### Core Components

1. **Configuration System** (`config.py`)
   - `ModelConfig`: Model parameters and settings
   - `TrainingConfig`: Training hyperparameters
   - `EnvironmentConfig`: Environment settings
   - `CacheConfig`: Cache directory management
   - `Config`: Main configuration class

2. **Models** (`models/`)
   - `PromptRewriter`: LLaMA-based prompt optimization
   - `EpicGA`: Genetic algorithm for text mutation
   - `CodeT5Model`: CodeT5+ model wrapper

3. **Agents** (`agents/`)
   - `PPOPolicy`: PPO policy network (actor-critic)
   - `PPOAgent`: PPO agent with experience buffer

4. **Environments** (`environments/`)
   - `RLPromptEnv`: Gymnasium environment for prompt optimization

5. **Utilities** (`utils/`)
   - `TextProcessor`: Text processing and validation
   - `CodeProcessor`: Code parsing and extraction
   - `CodeEvaluator`: Code execution and testing
   - `MetricsCalculator`: Performance metrics
   - `Logging`: Logging configuration
   - `FileUtils`: File I/O operations

### Key Features

- **Modular Design**: Clean separation of concerns
- **Configuration Management**: Flexible configuration system
- **CLI Interface**: Command-line tools for easy usage
- **Python API**: Programmatic interface for integration
- **Comprehensive Logging**: Detailed logging and monitoring
- **Error Handling**: Robust error handling and recovery
- **Extensibility**: Easy to extend and modify

## Usage Patterns

### 1. Command Line Interface
```bash
# Create configuration
ppo-codet5 config --output config.json

# Train model
ppo-codet5 train --config config.json

# Evaluate model
ppo-codet5 eval --checkpoint model.pt
```

### 2. Python API
```python
from ppo_codet5 import Config, PPOCodeT5Trainer

config = Config()
trainer = PPOCodeT5Trainer(config)
results = trainer.train()
```

### 3. Jupyter Notebook
```python
# Run original notebook for interactive development
jupyter notebook 01_ppo_codet5.ipynb
```

## Development Workflow

1. **Configuration**: Modify `config.py` for new settings
2. **Models**: Add new models in `models/` directory
3. **Agents**: Implement new RL agents in `agents/`
4. **Environments**: Create new environments in `environments/`
5. **Utilities**: Add utility functions in `utils/`
6. **Tests**: Write tests in `tests/` directory
7. **Examples**: Create examples in `examples/` directory

## Package Distribution

The package is designed for easy distribution and installation:

- **PyPI Ready**: Can be published to PyPI
- **Development Install**: `pip install -e .`
- **Production Install**: `pip install ppo-codet5`
- **Docker Support**: Ready for containerization
- **CI/CD Ready**: Automated testing and deployment

## Benefits of This Structure

1. **Professional**: Industry-standard Python package structure
2. **Maintainable**: Clear separation of concerns
3. **Extensible**: Easy to add new features
4. **Testable**: Comprehensive testing framework
5. **Documented**: Extensive documentation
6. **Deployable**: Ready for production use
7. **Collaborative**: Easy for team development

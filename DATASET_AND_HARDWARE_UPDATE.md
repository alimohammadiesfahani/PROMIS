# Dataset and Hardware Requirements Update

## Dataset Information Added

### MBPP (Microsoft Python Programming Benchmark)

- **Total Problems**: 974 programming problems
- **Training Split**: 374 samples
- **Loading Command**: `train_data = load_dataset("mbpp")["train"]`
- **Last prompt_id in CSV**: 974
- **Source**: [Microsoft Research MBPP Repository](https://github.com/microsoft/MBPP)

### Dataset Configuration
```python
# Dataset information now available in config
config.dataset.total_problems = 974
config.dataset.training_samples = 374
config.dataset.last_prompt_id = 974
config.dataset.load_command = 'load_dataset("mbpp")["train"]'
config.dataset.source_url = "https://github.com/microsoft/MBPP"
config.dataset.source_organization = "Microsoft Research"
```

## Hardware Requirements Updated

### System Requirements
- **Minimum**: 40GB VRAM for basic training
- **Recommended**: 80GB VRAM (NVIDIA A100 80GB PCIe)
- **Large-scale Training**: 80x NVIDIA A100 80GB PCIe for distributed training
- **Memory**: 32GB+ RAM (64GB+ recommended)
- **Storage**: 50GB+ free space

### Hardware Configuration
```python
# Training configuration
config.training.max_episodes = 1000  # Training episodes

# Environment configuration  
config.environment.max_samples = None  # Use all 374 training samples
```

## Attribution Links Added

### Organizations and Technologies
- **[Salesforce](https://www.salesforce.com/)** - [CodeT5+ model](https://huggingface.co/Salesforce/codet5p-770m-py)
- **[Microsoft Research](https://www.microsoft.com/en-us/research/)** - [MBPP dataset](https://github.com/microsoft/MBPP)
- **[Meta AI](https://ai.meta.com/)** - [LLaMA](https://github.com/facebookresearch/llama) and [CodeLlama](https://github.com/facebookresearch/codellama) models
- **[OpenAI](https://openai.com/)** - [PPO algorithm](https://openai.com/blog/openai-baselines-ppo/)
- **[Hugging Face](https://huggingface.co/)** - [Transformers library](https://github.com/huggingface/transformers)
- **[EPiC Framework](https://github.com/HamedTaherkhani/EPiC)** - Epic_GA component

## Files Updated

### Core Documentation
- `README.md` - Added dataset section, hardware requirements, attribution links
- `PROMIS_SUMMARY.md` - Added dataset info and hardware requirements
- `ppo_codet5/config.py` - Added DatasetConfig class with MBPP information

### Key Updates Made

1. **Dataset Section**: Added comprehensive MBPP dataset information
2. **Hardware Requirements**: Updated with specific VRAM requirements and A100 specifications
3. **Attribution Links**: Added proper links to all organizations and technologies
4. **Configuration**: Added DatasetConfig class for programmatic access to dataset info
5. **Training Parameters**: Clarified 1000 episodes and 374 training samples

## Training Configuration

### Dataset Loading
```python
from datasets import load_dataset

# Load MBPP dataset
train_data = load_dataset("mbpp")["train"]  # 374 samples
print(f"MBPP train size: {len(train_data)}")  # Output: 374
```

### Hardware Requirements
- **Basic Training**: 40GB VRAM minimum
- **Optimal Performance**: 80GB VRAM (NVIDIA A100 80GB PCIe)
- **Large-scale**: 80x NVIDIA A100 80GB PCIe for distributed training

## Impact Assessment

### Benefits
- **Clear Requirements**: Users know exactly what hardware they need
- **Proper Attribution**: All organizations and technologies properly credited
- **Dataset Clarity**: Clear information about MBPP dataset structure
- **Professional Presentation**: Academic-level documentation with proper citations

### Technical Considerations
- **Configuration**: Dataset information now available programmatically
- **Scalability**: Clear guidance for different training scales
- **Attribution**: Proper academic citations and links
- **Compatibility**: All existing functionality preserved

## Ready for Research

The project now provides:
- **Complete Dataset Information**: MBPP structure and loading details
- **Hardware Specifications**: Clear VRAM and system requirements
- **Proper Attribution**: Links to all contributing organizations
- **Academic Standards**: Professional documentation with citations
- **Configuration Support**: Programmatic access to dataset information

---

The project is now fully documented with dataset information, hardware requirements, and proper attribution to all contributing organizations and technologies.

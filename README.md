# Multilingual Translation Model for Low-Resource Languages

[![GitHub](https://img.shields.io/badge/GitHub-Data--science--projet-blue)](https://github.com/orgs/Data-science-projet/repositories)

## Project Overview
This project aims to develop a web-based translation application using HuggingFace Transformers to enable translation between French/English and low-resource languages (Bafia and Fulfulde). The project addresses the critical need for digital resources for low-resource languages and contributes to preserving linguistic heritage.

## Repository Structure
This project is organized into multiple repositories:
- [Frontend](https://github.com/Data-science-projet/Frontend): React-based web interface for translation
- [Translation_model](https://github.com/Data-science-projet/Translation_model): Core translation model implementation
- [Container-Orchestrer](https://github.com/Data-science-projet/Container-Orchestrer): Deployment and orchestration configuration

## Dataset

### Data Collection
- **Sources**:
  - Fulfulde Language:
    - Web-scraped Bible translations (English/French-Fulfulde)
    - SIL.org dictionary application database (Cameroonian linguistic company)
  - Bafia Language:
    - Web-scraped Bible translations (English/French-Bafia)

- **Data Types**: Text-based parallel corpora

- **Collection Challenges**:
  - Scarcity of digital text resources
  - Limited high-quality annotated data
  - Dialectal variations (Fulfulde Adamaoua vs. Fulfulde Burkina Faso)

- **Data Storage**: 
  - Initially: SQLite3
  - Subsequently: Google Spreadsheets in shared Google Drive

### Data Cleaning
- **Process**:
  - Created scripts to process web-scraped data into JSON format
  - Structured data with 'Source' and 'Target' fields
  - Processed application databases using custom scripts

- **Tools Used**:
  - Microsoft Excel
  - PyCharm

- **Quality Assessment**:
  - Automated: Find/replace methods for special characters, symbols, and numbers
  - Manual: Line-by-line review of parallel corpus

### Data Preprocessing
- **Alignment**: Sentence-level alignment
- **Tokenization**: BytePairEncoding using google-t5/t5-small pre-trained tokenizer
- **Data Split**:
  - Fulfulde Adamaoua:
    - Training: 29,000 sentences
    - Validation: 1,500 sentences
    - Test: 340 sentences
  - Bafia:
    - Training/Validation: ~10,000 sentences
    - Test: 426 sentences

- **Data Format**: Pandas DataFrames with source and target text columns

### Dataset Statistics
- **Bafia**: 10,426 highly annotated sentences
- **Fulfulde Adamaoua**: 
  - 30,840 sentences from Bible
  - 25,000 words from dictionary application

**Dataset Access**: Available on GitHub and Hugging Face

## Model Training

### Environment
- **Hardware**: T4 GPU High RAM
- **Software**:
  - Transformers
  - Datasets
  - PyTorch
  - SentencePiece
- **Platform**: Google Colab

### Architecture
- **Base Model**: google-t5/t5-small
- **Modifications**: None

### Training Parameters
```python
{
    "eval_strategy": "epoch",
    "learning_rate": 2e-5,
    "per_device_train_batch_size": 6,
    "per_device_eval_batch_size": 6,
    "save_total_limit": 2,
    "num_train_epochs": 10,
    "weight_decay": 0.01,
    "logging_dir": "./logs/{language}",
    "predict_with_generate": True,
    "logging_steps": 100,
    "save_strategy": "epoch"
}
```

### Training Process
- **Duration**: 6 hours
- **Monitoring**: Weight and Biases (Wandb.ai) for real-time metrics
- **Evaluation Metrics**: SACREBLEU, training loss, BLEU score, learning rate

## Evaluation

### Quantitative Results
- Fulfulde Language: BLEU score 2.46
- Fulfulde Adamaoua: BLEU score 0.37

### Qualitative Evaluation
- Human evaluation in progress
- Current evaluation based on BLEU Score

## Usage

### Model Access
The model is available on Hugging Face Hub and can be accessed through our [Translation_model](https://github.com/Data-science-projet/Translation_model) repository.

### Web Application
A live demo of the translation application is available through our [Frontend](https://github.com/Data-science-projet/Frontend) repository. The web interface allows users to:
- Translate text between French/English and Bafia/Fulfulde
- Access the translation model through a user-friendly interface
- View translation history and results

## Contributing
We welcome contributions to this project! Please follow these steps:

1. Fork the repository
2. Create a new branch for your feature
3. Make your changes
4. Submit a pull request

For detailed contribution guidelines, please refer to our [Contribution Guide](https://github.com/Data-science-projet/.github/blob/main/CONTRIBUTING.md).

## Citation
If you use this work in your research, please cite:

```bibtex
@misc{multilingual-translation-2024,
  author = {Data Science Project Team},
  title = {Multilingual Translation Model for Low-Resource Languages},
  year = {2024},
  publisher = {GitHub},
  url = {https://github.com/orgs/Data-science-projet/repositories}
}
```

## License
- **Code License**: MIT License
- **Dataset License**: Creative Commons Attribution 4.0 International
- **Model Weights License**: MIT License

## Acknowledgments
- SIL.org for their dictionary application
- The Data Science Project Team
- All contributors to the project

## Contact
- GitHub Issues: [Create an issue](https://github.com/Data-science-projet/.github/issues)
- Project Team: [Data Science Project Organization](https://github.com/orgs/Data-science-projet) 

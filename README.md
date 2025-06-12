
# HTS AI Agent 🤖

An intelligent AI agent for U.S. Harmonized Tariff Schedule (HTS) system that combines RAG-based question answering and duty calculation capabilities. Built with LangChain/CrewAI to assist trade professionals with tariff rules, duty rates, and policy agreements.

## 🌟 Features

### 1. RAG-Based Question Answering Agent
- Semantic search through HTS General Notes documentation
- Answers trade-related policy and agreement questions
- Provides citations from official documentation
- Built using LangChain's vector-based retrieval

### 2. HTS Duty Calculator Agent
- Processes HTS codes and product information
- Calculates duties based on multiple rate formats:
  - Percentage-based duties
  - Weight-based duties (¢/kg)
  - Unit-based duties ($/unit)
- Computes total landed cost
- Provides detailed duty breakdown

## 🛠️ Technical Stack

- **Framework**: LangChain/CrewAI
- **Vector Store**: FAISS/Chroma
- **Database**: SQLite/Postgres/DuckDB
- **Language**: Python 3.8+
- **Frontend**: Streamlit (Optional)

## 📋 Prerequisites

- Python 3.8 or higher
- Access to HTS documentation from hts.usitc.gov
- Section I CSV files from HTS
- Required Python packages (see requirements.txt)

## 🚀 Installation



1. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Download required data:
   - General Notes Full Documentation from hts.usitc.gov
   - Section I CSV files from HTS
   - Place in appropriate directories (see data/README.md)

## 💻 Usage

### RAG Agent
```python
from hts_agent.rag_agent import HTSRAGAgent

agent = HTSRAGAgent()
response = agent.query("What is United States-Israel Free Trade?")
print(response)
```

### Duty Calculator
```python
from hts_agent.duty_calculator import HTSDutyCalculator

calculator = HTSDutyCalculator()
result = calculator.calculate(
    hts_code="0101.30.00.00",
    product_cost=10000.0,
    freight=500.0,
    insurance=100.0,
    unit_weight=500.0,
    quantity=5
)
print(result)
```

## 📊 Sample Queries

### RAG Agent Examples:
1. "What is the United States-Israel Free Trade Agreement?"
2. "Can a product that exceeds its tariff-rate quota still qualify for duty-free entry under GSP or any FTA?"
3. "How is classification determined for an imported item that will be used as a part in manufacturing?"

### Duty Calculator Examples:
1. HTS code 0101.30.00.00, product cost $10,000, 500 kg weight, 5 units
2. "What's the HTS code for donkeys?"
3. "What are the applicable duty rates for female cattle?"

## 🏗️ Project Structure

```
hts-ai-agent/
├── data/                      # Data directory
│   ├── raw/                  # Raw HTS data
│   ├── processed/            # Processed data
│   └── vectors/              # Vector store
├── src/                      # Source code
│   ├── agents/              # Agent implementations
│   ├── tools/               # Custom tools
│   ├── utils/               # Utility functions
│   └── database/            # Database models
├── tests/                    # Test files
├── notebooks/               # Jupyter notebooks
├── requirements.txt         # Python dependencies
└── README.md               # This file
```

## 🔧 Configuration

1. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

2. Configure database:
```bash
python src/database/setup.py
```

## 🧪 Testing

Run the test suite:
```bash
pytest tests/
python -m src.cli rag --model google/flan-t5-base --pdf data/raw/general_notes.pdf "What is the United States-Israel Free Trade Agreement?"
python -m src.cli rag --model google/flan-t5-base --pdf data/raw/general_notes.pdf "Can a product that exceeds its tariff-rate quota still qualify for duty-free entry under GSP or any FTA? Why or why not?"
python -m src.cli rag --model google/flan-t5-base --pdf data/raw/general_notes.pdf "How is classification determined for an imported item that will be used as a part in manufacturing but isn’t itself a finished part?"
python -m src.cli tariff --hts 0101.30.00.00 --cost 10000 --freight 500 --insurance 100 --weight 500 --units 5
python -m src.cli rag --model google/flan-t5-base --pdf data/raw/general_notes.pdf "What’s the HTS code for donkeys?"
python -m src.cli rag --model google/flan-t5-base --pdf data/raw/general_notes.pdf "What are the applicable duty rates for female cattle?"
streamlit run src/streamlit_app.py

```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📫 Contact

Your Name - sairamreddy1511@gmail.com.com

Project Link:https://github.com/vuyyurusairamreddy/-HTSAgent-Task-sairamreddy

## 🙏 Acknowledgments

- U.S. International Trade Commission (USITC)
- LangChain/CrewAI community
- Open source contributors

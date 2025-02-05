# DeepSeek Search and Reasoning Agent with Pydantic AI

An intelligent agent system that combines DeepSeek's language models with search capabilities and structured outputs using Pydantic AI. This project demonstrates how to build a sophisticated research and reasoning system that can perform web searches, process information, and generate structured responses.

## 🌟 Features

- Integration with DeepSeek Chat and DeepSeek Reasoner models
- Structured data handling using Pydantic models
- Asynchronous web search capabilities using Tavily API
- Orchestration system for complex query processing
- Chain-of-thought reasoning extraction
- Formatted output generation

## 🛠️ Technologies Used

- **Pydantic AI**: For structured agent building and type validation
- **DeepSeek API**: Provides access to powerful language models
- **Tavily API**: For web search capabilities
- **Gemini API**: Used for output formatting
- **Nest AsyncIO**: Enables asynchronous operations in Jupyter notebooks
- **HTTPX**: For async HTTP requests

## 📋 Prerequisites

Before running this notebook, you'll need the following API keys:

- DEEPSEEK_API_KEY
- TAVILY_API_KEY
- GEMINI_API_KEY (for formatting agent)

## 🔧 Installation

```bash
pip install pydantic-ai
pip install nest_asyncio
pip install devtools
pip install tavily-python
```

## 🚀 Usage

### 1. Basic Search Setup

```python
from tavily import AsyncTavilyClient

tavily_client = AsyncTavilyClient(api_key=os.environ["TAVILY_API_KEY"])
```

### 2. Setting up DeepSeek Models

```python
deepseek_chat_model = OpenAIModel(
    'deepseek-chat',
    base_url='https://api.deepseek.com',
    api_key=os.environ["DEEPSEEK_API_KEY"],
)

deepseek_reasoner_model = OpenAIModel(
    'deepseek-reasoner',
    base_url='https://api.deepseek.com',
    api_key=os.environ["DEEPSEEK_API_KEY"],
)
```

### 3. Creating Structured Outputs

The project uses Pydantic models to ensure structured outputs:

```python
class ResearchResult(BaseModel):
    research_title: str
    research_main: str
    research_bullets: str
```

### 4. Using the Orchestrator

The orchestrator agent coordinates between different tools and models to produce comprehensive responses:

```python
orchestrator_agent = Agent(
    'google-gla:gemini-1.5-flash',
    result_type=ReportStructuredResult,
    system_prompt=ORCHESTRATOR_PROMPT
)
```

## 🏗️ Architecture

The system consists of several key components:

1. **Search Agent**: Handles web searches using Tavily API
2. **Reasoning Agent**: Uses DeepSeek Reasoner for deep analysis
3. **Formatting Agent**: Structures outputs using Gemini model
4. **Orchestrator**: Coordinates between all components

## 🔄 Workflow

1. User submits a query
2. Orchestrator generates search keywords
3. Search tool gathers relevant information
4. DeepSeek Reasoner processes and analyzes the information
5. Formatting agent structures the final output
6. Results are presented in a clear, organized format

## 📝 Example Usage

```python
# Set up dependencies
deps = SearchDataclass(max_results=3)

# Run a query
result = await orchestrator_agent.run(
    "Please create me a report on GRPO RL used in the DeepSeekR1-Zero model", 
    deps=deps
)

# Access structured results
print(result.data.title)
print(result.data.answer)
print(result.data.bullets)
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- DeepSeek team for their powerful language models
- Tavily for their search API
- Pydantic AI team for their structured agent framework

## ⚠️ Disclaimer

This project is for educational and research purposes. Please ensure you comply with all API terms of service and usage guidelines.

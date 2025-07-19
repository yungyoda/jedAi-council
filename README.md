# JedAI Stack - Powerful AI Agent Framework

🚀 **Build intelligent, collaborative AI agents with cutting-edge technology**

This repository provides a complete framework for creating sophisticated AI agents that can work together on complex tasks, powered by modern AI and graph technologies.

## 🛠️ Tech Stack

| Component | Purpose | Why It's Powerful |
|-----------|---------|-------------------|
| **[uv](https://docs.astral.sh/uv/)** | Package Manager | Lightning-fast Python package management - 10-100x faster than pip |
| **[CrewAI](https://crewai.com)** | Agent Framework | Multi-agent orchestration with role-based collaboration |
| **[Graphiti](https://github.com/graphiti-ai/graphiti)** | Graph RAG | Neo4j-powered knowledge graphs for intelligent information retrieval |
| **[LlamaIndex](https://www.llamaindex.ai/)** | Document Processing | Best-in-class document parsing and information extraction |

## 🚀 Quick Start

### Prerequisites
- Python 3.10 - 3.13
- [uv](https://docs.astral.sh/uv/) package manager

### Installation

1. **Install uv** (if you haven't already):
   ```bash
   # Windows
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   
   # macOS/Linux
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Clone and setup the project**:
   ```bash
   git clone <your-repo-url>
   cd jedAi-stack
   uv sync
   ```

3. **Configure your environment**:
   ```bash
   # Copy the example environment file
   cp .env.example .env
   
   # Add your API keys
   echo "OPENAI_API_KEY=your_openai_key_here" >> .env
   echo "NEO4J_URI=your_neo4j_uri" >> .env
   echo "NEO4J_USERNAME=your_username" >> .env
   echo "NEO4J_PASSWORD=your_password" >> .env
   ```

## 📚 uv vs Traditional Python

**Why uv?** It's the modern way to manage Python projects - faster, more reliable, and simpler.

| Traditional Python | uv (Modern) |
|-------------------|-------------|
| `python -m venv venv` | `uv sync` (automatic) |
| `venv\Scripts\activate` | `uv run` (no activation needed) |
| `pip install package` | `uv add package` |
| `requirements.txt` | `uv.lock` (automatic) |
| `pip freeze > requirements.txt` | Handled automatically |

## 🎯 Core Capabilities

### 1. Multi-Agent Collaboration (CrewAI)
Create specialized agents that work together:
```python
# Define agents with specific roles
researcher = Agent(
    role='Research Specialist',
    goal='Find and analyze relevant information',
    backstory='Expert in data gathering and analysis'
)

writer = Agent(
    role='Content Creator', 
    goal='Transform research into compelling content',
    backstory='Skilled writer with technical expertise'
)
```

### 2. Intelligent Knowledge Graphs (Graphiti)
Store and retrieve information using graph relationships:
```python
from graphiti import Graphiti

# Initialize graph memory
graph = Graphiti()

# Add knowledge with relationships
graph.add_episode(
    "The user asked about AI agents. AI agents are autonomous programs."
)

# Query with semantic understanding
results = graph.search("What are AI agents?")
```

### 3. Advanced Document Processing (LlamaIndex)
Extract insights from any document type:
```python
from llama_index import SimpleDirectoryReader, VectorStoreIndex

# Load and process documents
documents = SimpleDirectoryReader("./knowledge").load_data()
index = VectorStoreIndex.from_documents(documents)

# Query your documents
query_engine = index.as_query_engine()
response = query_engine.query("What are the key insights?")
```

## 🏗️ Project Structure

```
jedAi-stack/
├── src/jedai_council/           # Main application code
│   ├── config/                  # Agent and task configurations
│   │   ├── agents.yaml         # Define your AI agents
│   │   └── tasks.yaml          # Define agent tasks
│   ├── crew.py                 # Main crew orchestration
│   ├── main.py                 # Entry point
│   └── tools/                  # Custom tools for agents
├── knowledge/                   # Documents for processing
├── tests/                      # Test suite
├── pyproject.toml              # Project configuration
├── uv.lock                     # Locked dependencies
└── README.md                   # This file
```

## 🚀 Running Your Agents

### Basic Usage
```bash
# Run the default crew
uv run crewai run

# Or run with custom parameters
uv run python -m jedai_council.main
```

### Development Workflow
```bash
# Add new dependencies
uv add anthropic        # Add Claude AI
uv add --dev pytest     # Add development dependency

# Install/sync all dependencies
uv sync

# Run tests
uv run pytest

# Run specific scripts
uv run python scripts/your_script.py
```

## 🔧 Configuration

### 1. Environment Variables (.env)
```env
# Required
OPENAI_API_KEY=your_openai_api_key

# Optional - for Graph RAG
NEO4J_URI=bolt://localhost:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your_password

# Optional - for other LLM providers
ANTHROPIC_API_KEY=your_claude_key
COHERE_API_KEY=your_cohere_key
```

### 2. Agent Configuration (config/agents.yaml)
```yaml
researcher:
  role: "Senior Research Analyst"
  goal: "Uncover cutting-edge developments in AI and data science"
  backstory: |
    You're a seasoned researcher with a knack for uncovering the latest
    developments in AI and data science. You have a keen eye for detail.
  tools:
    - search_tool
    - graph_search_tool

writer:
  role: "Tech Content Strategist"  
  goal: "Craft compelling content on complex technical topics"
  backstory: |
    You're a skilled writer specializing in making complex technical
    topics accessible and engaging for diverse audiences.
  tools:
    - document_processor
```

### 3. Task Configuration (config/tasks.yaml)
```yaml
research_task:
  description: |
    Conduct comprehensive research on {topic}.
    Focus on recent developments and practical applications.
  expected_output: |
    A detailed research report with:
    - Key findings and insights
    - Recent developments
    - Practical applications
    - Reliable sources
  agent: researcher

writing_task:
  description: |
    Transform the research findings into an engaging article.
    Make complex topics accessible to a general audience.
  expected_output: |
    A well-structured article (1500+ words) with:
    - Compelling introduction
    - Clear explanations
    - Practical examples
    - Strong conclusion
  agent: writer
```

## 🎨 Advanced Features

### Custom Tools
Create specialized tools for your agents:
```python
from crewai_tools import tool

@tool
def knowledge_graph_search(query: str) -> str:
    """Search the knowledge graph for relevant information."""
    # Your custom graph search logic
    return results

@tool 
def document_analyzer(file_path: str) -> str:
    """Analyze documents using LlamaIndex."""
    # Your document processing logic
    return analysis
```

### Multi-Modal Processing
```python
# Process different file types
from llama_index import (
    SimpleDirectoryReader,
    PDFReader, 
    DocxReader,
    ImageReader
)

# Support for PDFs, Word docs, images, etc.
reader = SimpleDirectoryReader(
    input_dir="./knowledge",
    file_extractor={
        ".pdf": PDFReader(),
        ".docx": DocxReader(), 
        ".jpg": ImageReader(),
        ".png": ImageReader(),
    }
)
```

## 🧪 Examples

### Example 1: Research Assistant
```bash
# Run research on a specific topic
uv run crewai run --topic "Latest developments in Large Language Models"
```

### Example 2: Document Analysis
```python
# Process and analyze documents in knowledge folder
uv run python examples/document_analysis.py
```

### Example 3: Interactive Agent Chat
```python
# Start interactive session with your agents
uv run python examples/interactive_chat.py
```

## 📈 Performance Tips

1. **Use Graph RAG** for better context retention across conversations
2. **Chunk documents** appropriately for LlamaIndex processing
3. **Cache frequently used** embeddings and graph queries
4. **Monitor token usage** across different LLM providers
5. **Use async operations** for concurrent agent tasks

## 🛠️ Development

### Adding New Agents
1. Define agent in `config/agents.yaml`
2. Create corresponding tasks in `config/tasks.yaml`
3. Add any custom tools in `src/jedai_council/tools/`
4. Update crew configuration in `crew.py`

### Testing
```bash
# Run all tests
uv run pytest

# Run specific test categories
uv run pytest tests/agents/
uv run pytest tests/tools/
```

### Contributing
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Add tests for new functionality
5. Run tests: `uv run pytest`
6. Commit changes: `git commit -m 'Add amazing feature'`
7. Push to branch: `git push origin feature/amazing-feature`
8. Open a Pull Request

## 🔍 Troubleshooting

### Common Issues

**Dependencies not installing?**
```bash
# Clear cache and retry
uv cache clean
uv sync --reinstall
```

**Environment variables not loading?**
```bash
# Make sure .env file exists and has correct format
cp .env.example .env
# Edit .env with your actual API keys
```

**Graph database connection issues?**
```bash
# Check Neo4j is running
docker run -p 7474:7474 -p 7687:7687 neo4j:latest
```

**Memory issues with large documents?**
```python
# Process documents in chunks
from llama_index import SimpleDirectoryReader
reader = SimpleDirectoryReader("./knowledge", chunk_size=512)
```

## 📚 Resources

### Documentation
- [CrewAI Documentation](https://docs.crewai.com)
- [LlamaIndex Documentation](https://docs.llamaindex.ai)
- [Graphiti Documentation](https://github.com/graphiti-ai/graphiti)
- [uv Documentation](https://docs.astral.sh/uv/)

### Community
- [CrewAI Discord](https://discord.com/invite/X4JWnZnxPb)
- [LlamaIndex Discord](https://discord.gg/dGcwcsnxhU)
- [uv GitHub Discussions](https://github.com/astral-sh/uv/discussions)

### Tutorials
- [Building Multi-Agent Systems](https://docs.crewai.com/how-to/Creating-a-Crew-and-kick-it-off)
- [Graph RAG with Neo4j](https://neo4j.com/developer/graph-data-science/)
- [LlamaIndex QuickStart](https://docs.llamaindex.ai/en/stable/getting_started/starter_example.html)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **CrewAI** team for the excellent multi-agent framework
- **LlamaIndex** community for document processing capabilities  
- **Graphiti** developers for graph-based RAG implementation
- **Astral** team for the lightning-fast uv package manager

---

**Ready to build the future with AI agents?** 🤖✨

Start by running `uv sync` and then `uv run crewai run` to see your agents in action!

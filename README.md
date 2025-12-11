 🌐 Agent Referee System

The Agent Referee System is a full-stack multi-agent reasoning framework designed to ensure high-
quality, validated AI responses. It consists of a modern Tailwind-powered frontend, a FastAPI backend
orchestrating a 4-agent workflow, and a Gemini-based Referee that validates decisions.

## ✨ Features

🧠 Multi-Agent Reasoning Pipeline
The system processes user queries through a chain of specialized agents:

1. Primary Solver: Generates the initial full solution.
2. Logic Critic: Checks for logical consistency and fallacies.
3. Domain Expert: Validates factual correctness.
4. Optimizer: Produces the refined final output.

🔎 Gemini Referee System
A strict judging layer that acts as the final gatekeeper. It returns a structured JSON verdict:


{
"verdict": "VALID | INVALID",
"reason": "Explanation of the decision...",
"required_fixes": ["List of specific issues to address"],
"confidence_score": 85
}

💾 Vector Memory (Qdrant)
Stores validated agent outputs to enable retrieval-augmented reasoning (RAG) for future queries.

🖥 Modern Frontend UI
Chat interface
Expandable workflow step panels
Markdown rendering + Syntax highlighting
Animated agent activity indicators

⚙ Backend Stack
Framework: FastAPI
Orchestration: LangChain & LangGraph
Models: Ollama (Agents) & Google Gemini (Referee)
Storage: Qdrant (Vector DB) & Redis (Caching/Queue)

## 📁 Project Structure
/
├── index.html # Frontend UI (Tailwind, Marked.js, Highlight.js) 
#
└── main.py # FastAPI backend with multi-agent workflow + referee
#

## 🚀 Setup Instructions

󾠮 Install Dependencies


pip install fastapi uvicorn langchain langchain-ollama langchain-google-genai \
langchain-qdrant qdrant-client redis

󾠯 Start Infrastructure (Qdrant & Redis)


docker run -p 6333:6333 qdrant/qdrant
docker run -p 6379:6379 redis

󾠰 Pull Local Model (Ollama)


ollama pull qwen2.5:7b-instruct

󾠱 Set Google API Key
Required for the Gemini Referee.


export GOOGLE_API_KEY="YOUR_KEY_HERE"

󾠲 Run Backend


uvicorn main:app --reload --host 0.0.0.0 --port 8000

󾠳 Run Frontend
Simply open index.html in your web browser.

## 🔄 API Endpoints

Run Workflow
POST /run Executes the multi-agent reasoning loop.

Request Body:



{
"query": "Explain the significance of the Riemann Hypothesis.",
"max_retries": 2
}

Response:
final_response: The optimized answer.
history: Detailed breakdown of agent steps and referee decisions.

Health Check
GET /health Basic service status check.

## 🛠 Configuration

Model Settings
You can modify the models in main.py:


OLLAMA_MODEL = "qwen2.5:7b-instruct"
GEMINI_MODEL = "gemini-2.5-flash"

Workflow Settings


MAX_RETRIES = 2

Frontend Connection
Update the API URL in index.html if your backend is running elsewhere:


const API_URL = "[http://10.224.148.61:8000/run](http://10.224.148.61:8000/run)";

## 📝 Future Enhancements


[ ] Redis caching implementation
[ ] Improved memory retrieval strategies
[ ] User Authentication for Gemini usage
[ ] Streaming responses via WebSockets

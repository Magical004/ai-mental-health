# Mental Health Chatbot 🤖💚

A RAG-powered mental health assistant with multilingual support, voice capabilities, and empathetic AI responses. Built with Groq API, ChromaDB, and modern AI technologies.

## 🌟 Features

- **🤖 AI-Powered Conversations**: RAG architecture with Llama 3.3 70B model
- **🌍 Multilingual Support**: 133 languages with automatic translation
- **🎤 Voice Interface**: Text-to-speech and speech-to-text capabilities
- **💬 Conversation Memory**: Context-aware responses with session management
- **⚡ High Performance**: Groq LPU technology for <100ms responses
- **🔒 Privacy-Focused**: Local vector database with synthetic data generation

## 🏗️ Architecture

```
Frontend (Web/CLI) → FastAPI Server → RAG Layer → Groq API → Response
      ↑               ↓          ↑         ↓
   Voice I/O     ChromaDB    Translation   Mental Health
                 Knowledge     Layer         Knowledge
```

## 📦 Installation

### Prerequisites
- Python 3.10+
- Groq API account
- (Optional) ElevenLabs account for premium TTS

### 1. Clone Repository
```bash
git clone https://github.com/harjas-romana/capstone-one
```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Environment Setup
```bash
cp .env.example .env
```

Edit `.env` file:
```env
# Required
GROQ_API_KEY=your_groq_api_key_here

# Optional (for premium voice)
ELEVENLABS_API_KEY=your_elevenlabs_api_key
```

### 5. Get API Keys
- **Groq API**: https://console.groq.com/
- **ElevenLabs** (optional): https://elevenlabs.io/

## 🚀 Quick Start

### Option 1: Web Server (Recommended)
```bash
python server.py
```
Access at: http://localhost:8000
- API Docs: http://localhost:8000/docs
- Health Check: http://localhost:8000/health

### Option 2: CLI Interface
```bash
python agent.py
```

### Option 3: Voice Interface
```bash
python voice.py
```

## 📚 API Usage

### Basic Chat
```bash
curl -X POST "http://localhost:8000/chat" \
  -H "Content-Type: application/json" \
  -d '{"message": "I feel anxious today", "language": "en"}'
```

### Voice Chat with Audio
```bash
curl -X POST "http://localhost:8000/voice/chat" \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello", "language": "en", "generate_audio": true}'
```

### Text-to-Speech
```bash
curl -X POST "http://localhost:8000/voice/text-to-speech" \
  -H "Content-Type: application/json" \
  -d '{"text": "Hello, how can I help you?", "language": "en"}'
```

### Speech-to-Text
```bash
curl -X POST "http://localhost:8000/voice/speech-to-text" \
  -F "audio_file=@recording.wav"
```

## 🗣️ Voice Commands (CLI)

In voice mode, you can use these commands:
- `"help"` - Show available commands
- `"new chat"` - Start fresh conversation
- `"change language"` - Switch language
- `"exit"` - Quit the program

## 🌍 Supported Languages

The system supports 133 languages including:
- English (`en`), Spanish (`es`), French (`fr`)
- German (`de`), Italian (`it`), Hindi (`hi`)
- Chinese (`zh`), Japanese (`ja`), Arabic (`ar`)
- And 124 more!

## 🏗️ Project Structure

```
mental-health-chatbot/
├── server.py          # FastAPI web server
├── agent.py           # CLI chat interface
├── voice.py           # Voice interface
├── rag_layer.py       # RAG system with ChromaDB
├── dataset.py         # Synthetic data generation
├── requirements.txt   # Python dependencies
├── .env.example       # Environment template
└── README.md          # This file
```

## 🔧 Configuration

### Environment Variables
```env
# Required
GROQ_API_KEY=your_groq_api_key

# Optional
ELEVENLABS_API_KEY=your_elevenlabs_key
CHROMA_DB_PATH=./chroma_mentalhealth_db
LOG_LEVEL=INFO
```

### Custom Knowledge Base
Edit the sample data in `rag_layer.py` to add your own mental health knowledge:

```python
sample_documents = [
    {
        "text": "Your custom mental health knowledge here...",
        "source": "Custom Source",
        "type": "condition",
        "metadata": {"condition": "custom"}
    }
]
```

## 🐛 Troubleshooting

### Common Issues

1. **API Key Errors**
   ```bash
   export GROQ_API_KEY=your_actual_key_here
   ```

2. **Audio Issues on macOS**
   ```bash
   brew install portaudio
   pip install pyaudio
   ```

3. **Port Already in Use**
   ```bash
   python server.py --port 8080
   ```

4. **Module Not Found**
   ```bash
   pip install -r requirements.txt
   ```

### Logs
- Server logs: `mental_health_server.log`
- Application logs: Console output

## 🚀 Deployment

### Production Deployment
```bash
# Use production server
uvicorn server:app --host 0.0.0.0 --port 8000 --workers 4

# Or with gunicorn
gunicorn -w 4 -k uvicorn.workers.UvicornWorker server:app
```

### Docker Deployment
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY . .
RUN pip install -r requirements.txt

EXPOSE 8000
CMD ["python", "server.py"]
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Development
```bash
# Format code
black *.py

# Lint code
flake8 *.py

# Run tests
pytest tests/
```

## 📊 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Home page with API information |
| `GET` | `/health` | Server health check |
| `POST` | `/chat` | Main chat endpoint |
| `POST` | `/voice/chat` | Voice chat with audio |
| `POST` | `/voice/tts` | Text-to-speech conversion |
| `POST` | `/voice/stt` | Speech-to-text conversion |
| `GET` | `/languages` | List supported languages |
| `POST` | `/translate` | Text translation |
| `GET` | `/sessions` | List active sessions |
| `DELETE` | `/sessions/{id}` | Delete session |

## ⚠️ Disclaimer

This is a personal project developed for educational purposes. It is **not a substitute for professional mental health care**. 

**For serious mental health concerns:**
- Contact licensed professionals
- Use emergency services when needed
- Call crisis hotlines: 988 (US), 116123 (EU)

## 📞 Crisis Resources

- **National Suicide Prevention Lifeline**: 988 or 1-800-273-8255
- **Crisis Text Line**: Text "HOME" to 741741
- **Emergency Services**: 911 or local emergency number

## 👥 Developer
- Danish Mahajan



## 🙏 Acknowledgments

- Groq Inc. for LPU technology and API access
- Meta for Llama 3.3 70B model
- ElevenLabs for text-to-speech services
- ChromaDB team for vector database
- Open-source community for various libraries

---

**Note**: This project is for educational purposes only. Always consult qualified healthcare professionals for mental health concerns.

*Documented by Danish Mahajan*

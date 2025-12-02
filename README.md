📚 Talk2Books — Multilingual RAG App

🤖 Ask questions from your uploaded books or documents — in English, Hindi, or Punjabi — and get AI-powered answers in any of these languages!

Talk2Books is a Retrieval-Augmented Generation (RAG) system built with LangChain, FAISS, and Ollama.
It uses local embeddings, language detection, and translation to understand and answer questions from uploaded text files — no external APIs required.

✨ Features

✅ Upload up to 5 text/PDF/DOCX files
✅ Multi-language support — English, Hindi, Punjabi
✅ Choose question and answer language independently
✅ Automatic language detection and translation
✅ Local inference using Ollama models (e.g., qwen2.5:3b)
✅ Stores uploaded files temporarily — deleted after session
✅ Modern, clean frontend UI built with HTML/CSS/JS
✅ Backend powered by Quart (async Flask) and LangChain

🏗️ Tech Stack
Component	Technology
Frontend	HTML, CSS, Vanilla JavaScript
Backend	Python, Quart, Quart-CORS
AI/RAG Framework	LangChain Core + Community + FAISS
Embeddings	Sentence Transformers (all-MiniLM-L6-v2)
LLM	Ollama (qwen2.5:3b)
Language Translation	Deep Translator
Vector Store	FAISS (local)
Environment	Python 3.10+
📂 Project Structure
talk2books/
├── backend/
│   ├── app.py                   # Main Quart server
│   ├── rag_chain.py             # RAG + translation logic
│   ├── loaders.py               # Document loading & splitting
│   ├── requirements.txt         # Dependencies
│   ├── run_backend.bat          # Windows start script
│   ├── run_backend.sh           # Linux/Mac start script
│   ├── sample_docs/             # Uploaded files stored temporarily
│
└── frontend/
    ├── index.html               # UI for upload and Q&A
    ├── script.js                # Frontend logic (upload + ask)
    └── style.css                # UI styling

⚙️ Setup Instructions
🧩 Prerequisites

Python 3.10 or newer

(Optional) Ollama
 installed with model qwen2.5:3b

ollama pull qwen2.5:3b


Git (for cloning)

🪄 1. Clone the Repository
git clone https://github.com/<your-username>/talk2books.git
cd talk2books/backend

🧱 2. Create a Virtual Environment
Windows:
python -m venv .venv
.venv\Scripts\activate

macOS/Linux:
python3 -m venv .venv
source .venv/bin/activate

📦 3. Install Dependencies
pip install --upgrade pip
pip install -r requirements.txt

▶️ 4. Run the Backend
python app.py


If successful, you’ll see:

🚀 Starting Talk2Books backend (multi-language, temp session mode)...
 * Running on http://0.0.0.0:5000

🌐 5. Launch the Frontend

Open the file manually:

talk2books/frontend/index.html


Or run a local server:

cd ../frontend
python -m http.server 5500


Then visit → http://localhost:5500

🧠 How It Works

Upload up to 5 files (any combination of .txt, .pdf, .docx).

The system detects their language using langdetect.

Texts are split into chunks and embedded via sentence-transformers.

FAISS builds a vector index for fast retrieval.

When you ask a question:

The question language is auto-detected.

It is translated to English for consistent retrieval.

The top chunks are fetched via FAISS.

Ollama’s qwen2.5:3b generates an answer.

The final answer is translated back into your selected answer language.

🧾 Example Use
Input	Output
Question (Hindi): अर्जुन कौन था?
Answer Language: English	“Arjuna was one of the Pandava brothers in the Mahabharata...”
Question (English): Who is Guru Nanak Dev Ji?
Answer Language: Punjabi	“ਗੁਰੂ ਨਾਨਕ ਦੇਵ ਜੀ ਸਿੱਖ ਧਰਮ ਦੇ ਸੰਸਥਾਪਕ ਸਨ…”
💻 Run Scripts (Optional)
Windows (auto setup)

Double-click run_backend.bat

macOS/Linux
chmod +x run_backend.sh
./run_backend.sh

🧹 Cleanup & Session Handling

Uploaded files are stored temporarily in backend/sample_docs/

On server restart or after session ends → all uploads are deleted automatically.

🚀 Deployment Options
🧩 Local Environment

Use Python venv as shown above.

🐳 Docker (Optional)

Add this Dockerfile inside /backend:

FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]


Then build & run:

docker build -t talk2books .
docker run -p 5000:5000 talk2books

🧰 Troubleshooting
Problem	Fix
ModuleNotFoundError: No module named 'langchain.text_splitter'	Run pip install -U langchain-text-splitters
FAISS list index out of range	Make sure at least one valid document is uploaded
LLM not found (Ollama)	Run ollama pull qwen2.5:3b before starting backend
Answer not in target language	Ensure deep-translator is installed and working properly
Network error in browser	Backend must run at localhost:5000; check CORS in app.py
📜 License

This project is open-source under the MIT License — free to use, modify, and share.

👩‍💻 Author

Developed by Sanya
💬 Inspired by the idea of bridging language diversity with AI.

If you like this project, give it a ⭐ on GitHub
 and share it with others!

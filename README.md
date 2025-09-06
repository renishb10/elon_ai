🧩 Elon-AI | Simple LangChain Summarizer
A tiny Python app that uses LangChain + OpenAI Chat API to turn a block of biography text into:

a short summary, and
two interesting facts.
✨ What it does
Builds a PromptTemplate that asks for a summary + two facts.
Pipes the prompt into an OpenAI chat model via ChatOpenAI.
Prints the model’s response to the console.
Entrypoint: main() in app.py.

📁 Project structure (suggested)
.
├─ app.py # your script (the code you shared)
├─ requirements.txt # pinned deps (see below)
└─ .env # your API key (not committed)
✅ Prerequisites
Python 3.9+
An OpenAI-compatible API key set in your environment (see .env below)
📦 Install

# 1) Create & activate a virtual environment (recommended)

python -m venv .venv

# Windows: .venv\Scriptsctivate

source .venv/bin/activate

# 2) Install dependencies

pip install -U pip
pip install -r requirements.txt
requirements.txt

langchain>=0.2
langchain-openai>=0.2
python-dotenv>=1.0
If you don’t want a requirements.txt, you can install directly: pip install langchain langchain-openai python-dotenv

🔐 Environment variables
Create a .env file in the project root:

OPENAI_API_KEY=sk-your-key-here

# Optional: point to a compatible server, if not using OpenAI

# OPENAI_BASE_URL=https://api.your-compatible-endpoint.com/v1

The app uses python-dotenv to load this automatically.

▶️ Run
python app.py
You’ll see output like:

Short summary:
...

Two interesting facts:

1. ...
2. ...
   ⚙️ How it works (quick tour)
   PromptTemplate
   Formats the instruction:

Given the information {information} ...

1. A Short summary
2. Two interesting facts ...
   ChatOpenAI
   A LangChain wrapper for the OpenAI Chat API:

llm = ChatOpenAI(model="gpt-5", temperature=0)
Don’t have access to gpt-5? Replace with any chat-capable model you can use (e.g., gpt-4o-mini, gpt-4o, etc.).

Chain composition
Uses the pipe operator to compose prompt -> llm, then:

response = chain.invoke({"information": information})
print(response.content)
🛠️ Customize
Model: ChatOpenAI(model="gpt-4o")
Creativity: temperature=0.7 for more variety
Prompt: Ask for bullets, JSON, tone/length limits, etc.
Input: Replace the information string with your own text
🧪 Example: return JSON (optional)
If you prefer structured output, tweak the prompt:

summary_template = """
Given the information {information}, return valid JSON:
{
"summary": "<one short paragraph>",
"facts": ["<fact 1>", "<fact 2>"]
}
"""
Then parse response.content as JSON.

🩺 Troubleshooting
InvalidRequestError: model not found
You don’t have access to that model. Choose one you do.
401 Unauthorized
Check OPENAI_API_KEY in .env is set and loaded.
Rate limits / costs
Large inputs cost more—trim or summarize upstream.
🔒 Safety & privacy
Don’t commit .env to version control.
Review text you send to the API for sensitive data.
📄 License
Use, modify, or adapt freely in your projects. Add a license if you publish.

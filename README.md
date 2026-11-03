# Simple Research Agent

A beginner project that builds a small AI research agent in a Jupyter notebook. The agent receives a topic, decides what to search for, calls a web search tool, reads the results, and writes a short report with sources.

## How it works

The agent is made of three parts:

| Part | What it does | Used here |
|---|---|---|
| Brain | Decides what to do and writes the answer | A free model through OpenRouter (Groq and Gemini also supported) |
| Tool | Searches the web | Tavily |
| Loop | Connects the two | A Python function in the notebook |

The loop works like this:

1. Send the question to the model.
2. If the model asks to use the search tool, run the search and send the results back.
3. Repeat until the model replies with text instead of a tool request.
4. That text is the final report.

A `max_steps` limit stops the agent from looping forever.

## Files

- `research_agent_free.ipynb` - the notebook
- `requirements.txt` - the Python libraries needed
- `.gitignore` - keeps secret keys and the virtual environment out of Git

## Setup

You need Python 3.10 or newer. I used Python 3.13. Python 3.15 failed to install some libraries because they had no ready-made packages for it yet.

1. Clone or download this repository and open a terminal in its folder.

2. Create and activate a virtual environment.

   Windows (PowerShell):

   ```
   py -3.13 -m venv venv
   venv\Scripts\Activate.ps1
   ```

   Mac/Linux:

   ```
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install the libraries:

   ```
   pip install -r requirements.txt
   ```

4. Create a file named `.env` in the same folder with your own keys:

   ```
   TAVILY_API_KEY=your_key_here
   OPENROUTER_API_KEY=your_key_here
   ```

   Groq and Gemini are optional alternatives. Add `GROQ_API_KEY` or `GEMINI_API_KEY` if you want to use them.

5. Open the notebook in VS Code or Jupyter, select the `venv` kernel, and run the cells from top to bottom.

## Choosing a provider

In the first code cell, change this line:

```python
PROVIDER = 'openrouter'   # options: 'groq', 'gemini', 'openrouter'
```

Free tiers and model names change over time. If you see a "model not found" error, look up a current model name in the provider's dashboard and update the `model` value in the `PROVIDERS` dictionary.



## Ideas for next steps

- Add a reflection step where the model critiques and improves its own report.
- Add a second tool that fetches a full web page.
- Write a few test topics and check that each report includes sources.

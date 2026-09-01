# CodeAlpha-
Language Translation Tool Features: Enter text to translate Select source and target language Translate using an API Display translated text Copy translated text Clean, responsive UI  
from flask import Flask, render_template, request
from deep_translator import GoogleTranslator

app = Flask(__name__)

languages = {
    "English": "en",
    "Hindi": "hi",
    "Marathi": "mr",
    "French": "fr",
    "German": "de",
    "Spanish": "es",
    "Japanese": "ja",
    "Chinese": "zh-CN"
}

@app.route("/", methods=["GET", "POST"])
def home():
    translated = ""

    if request.method == "POST":
        text = request.form["text"]
        source = request.form["source"]
        target = request.form["target"]

        translated = GoogleTranslator(
            source=source,
            target=target
        ).translate(text)

    return render_template(
        "index.html",
        languages=languages,
        translated=translated
    )

if __name__ == "__main__":
    app.run(debug=True)
    <!DOCTYPE html>
<html>
<head>
    <title>Language Translator</title>

    <style>
        body {
            font-family: Arial;
            background: #f2f2f2;
            text-align: center;
            padding: 50px;
        }

        .container {
            background: white;
            max-width: 600px;
            margin: auto;
            padding: 30px;
            border-radius: 15px;
        }

        textarea {
            width: 90%;
            height: 120px;
            padding: 10px;
            margin: 15px;
        }

        select, button {
            padding: 10px;
            margin: 10px;
        }

        button {
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .result {
            background: #eee;
            padding: 15px;
            margin-top: 20px;
            min-height: 50px;
        }
    </style>
</head>

<body>

<div class="container">

    <h1>🌐 Language Translator</h1>

    <form method="POST">

        <textarea name="text"
                  placeholder="Enter text here..."
                  required></textarea>

        <br>

        <select name="source">
            <option value="auto">Auto Detect</option>

            {% for name, code in languages.items() %}
                <option value="{{ code }}">{{ name }}</option>
            {% endfor %}
        </select>

        ➡️

        <select name="target">
            {% for name, code in languages.items() %}
                <option value="{{ code }}">{{ name }}</option>
            {% endfor %}
        </select>

        <br>

        <button type="submit">Translate</button>

    </form>

    {% if translated %}
        <div class="result">
            <h3>Translation:</h3>
            <p id="translation">{{ translated }}</p>

            <button onclick="copyText()">Copy</button>

            <button onclick="speakText()">🔊 Speak</button>
        </div>
    {% endif %}

</div>

<script>
function copyText() {
    let text = document.getElementById("translation").innerText;
    navigator.clipboard.writeText(text);
    alert("Copied!");
}

function speakText() {
    let text = document.getElementById("translation").innerText;
    let speech = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(speech);
}
</script>

</body>
</html>
LinguaFlow — Language Translation Tool
A modern, responsive web-based language translation tool built with Python, Flask, HTML, CSS and JavaScript. It lets users enter text, choose source and target languages, and receive a translated result through the Google translation service used by deep-translator.
✨ Features
🌍 Translate between 18+ languages
🔎 Auto-detect source language
⚡ Simple AJAX translation without page reload
📱 Responsive modern UI
🔢 5,000-character input limit
🔄 Swap source and target languages
📋 Easy-to-copy translated result
🎨 Clean card-based interface
❌ Friendly error handling
🛠️ Tech Stack
Python 3
Flask
deep-translator
HTML5
CSS3
JavaScript (Fetch API)
📁 Project Structure
language_translation_tool/
├── app.py
├── requirements.txt
├── README.md
├── screenshots/
│   └── .gitkeep
├── templates/
│   └── index.html
└── static/
    ├── style.css
    └── script.js
🚀 Installation
1. Clone the repository
git clone https://github.com/YOUR_USERNAME/language-translation-tool.git
cd language-translation-tool
2. Create a virtual environment (recommended)
Windows:
python -m venv venv
venv\Scripts\activate
macOS/Linux:
python3 -m venv venv
source venv/bin/activate
3. Install dependencies
pip install -r requirements.txt
4. Run the application
python app.py
Open http://127.0.0.1:5000 in your browser.
📸 Screenshots
Add your screenshots to the screenshots/ folder and update the paths below:
Home Page
�
Translation Result
�
Tip: Take screenshots after running the project locally. This keeps the README honest and shows your own working application.
🧪 Example
Input: Hello, how are you?
Target: Hindi
Output: नमस्ते, आप कैसे हैं?
🔮 Future Improvements
Text-to-speech button with language-aware voices
Translation history
Dark mode
User accounts
More translation providers
File/document translation
Deploy on Render, Railway or PythonAnywhere
⚠️ Note
deep-translator accesses online translation services, so an internet connection is required. Availability and behavior of third-party translation services can change.
👩‍💻 Author
Jigyasa Kumbhare
B.Tech CSE-AIML Student
📄 License
This project is intended for educational and internship purposes. Add an MIT license if you decide to distribute it as open-source.

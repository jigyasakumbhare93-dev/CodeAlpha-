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
</html>I

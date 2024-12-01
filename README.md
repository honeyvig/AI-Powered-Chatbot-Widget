# AI-Powered-Chatbot-Widget

Here's a Python implementation to create an AI-powered chatbot widget for a website. This solution uses Flask for the backend, integrates OpenAI's GPT for natural language processing, and provides a frontend using HTML, CSS, and JavaScript to embed the chatbot widget.
Code Implementation
Backend (Flask)

from flask import Flask, request, jsonify
import openai

# Initialize Flask app
app = Flask(__name__)

# OpenAI API Key
openai.api_key = "your_openai_api_key"

# Endpoint for chatbot interaction
@app.route('/chat', methods=['POST'])
def chat():
    user_message = request.json.get("message", "")
    if not user_message:
        return jsonify({"error": "Message is required"}), 400

    # OpenAI API call
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[
                {"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": user_message},
            ]
        )
        chatbot_reply = response["choices"][0]["message"]["content"]
        return jsonify({"reply": chatbot_reply})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == '__main__':
    app.run(debug=True)

Frontend (HTML + CSS + JavaScript)

Create a file named index.html:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot Widget</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .chat-widget {
            width: 300px;
            height: 400px;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: white;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .chat-header {
            background-color: #0078d7;
            color: white;
            padding: 10px;
            text-align: center;
        }
        .chat-body {
            flex: 1;
            padding: 10px;
            overflow-y: auto;
            border-top: 1px solid #ccc;
        }
        .chat-input {
            display: flex;
            border-top: 1px solid #ccc;
        }
        .chat-input textarea {
            flex: 1;
            border: none;
            padding: 10px;
            resize: none;
        }
        .chat-input button {
            background-color: #0078d7;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="chat-widget">
        <div class="chat-header">Chat with us</div>
        <div class="chat-body" id="chatBody"></div>
        <div class="chat-input">
            <textarea id="userMessage" placeholder="Type your message..."></textarea>
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>

    <script>
        async function sendMessage() {
            const userMessage = document.getElementById("userMessage").value;
            if (!userMessage.trim()) return;

            // Display user's message
            const chatBody = document.getElementById("chatBody");
            const userDiv = document.createElement("div");
            userDiv.textContent = "You: " + userMessage;
            chatBody.appendChild(userDiv);
            document.getElementById("userMessage").value = "";

            // Call backend API
            try {
                const response = await fetch('/chat', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ message: userMessage })
                });

                const data = await response.json();
                const botDiv = document.createElement("div");
                botDiv.textContent = "Bot: " + (data.reply || "Error in response");
                chatBody.appendChild(botDiv);
                chatBody.scrollTop = chatBody.scrollHeight;
            } catch (error) {
                const errorDiv = document.createElement("div");
                errorDiv.textContent = "Error: Unable to reach the server.";
                chatBody.appendChild(errorDiv);
            }
        }
    </script>
</body>
</html>

Steps to Run:

    Install Dependencies:

pip install flask openai

Set OpenAI API Key: Replace "your_openai_api_key" in the backend code with your actual OpenAI API key.
Run Flask Server:

    python app.py

    Host Frontend: Place the index.html file in the same directory or serve it through a local web server.
    Open in Browser: Access the chatbot widget on your website, connected to the Flask backend.

Features:

    User Engagement: Real-time interaction with visitors.
    Customizable Responses: Tailored to your FAQs and support needs.
    Scalable Backend: OpenAI's API ensures intelligent, context-aware replies.

Future Enhancements:

    Persistent Conversations: Store chat history using a database (e.g., SQLite, PostgreSQL).
    Multi-language Support: Enable the chatbot to understand and reply in multiple languages.
    Integration: Connect to CRM tools for customer tracking or analytics platforms to analyze usage.
===================
ChatGPT said:
ChatGPT

Here's a Python implementation to create an AI-powered chatbot widget for a website. This solution uses Flask for the backend, integrates OpenAI's GPT for natural language processing, and provides a frontend using HTML, CSS, and JavaScript to embed the chatbot widget.
Code Implementation
Backend (Flask)

from flask import Flask, request, jsonify
import openai

# Initialize Flask app
app = Flask(__name__)

# OpenAI API Key
openai.api_key = "your_openai_api_key"

# Endpoint for chatbot interaction
@app.route('/chat', methods=['POST'])
def chat():
    user_message = request.json.get("message", "")
    if not user_message:
        return jsonify({"error": "Message is required"}), 400

    # OpenAI API call
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[
                {"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": user_message},
            ]
        )
        chatbot_reply = response["choices"][0]["message"]["content"]
        return jsonify({"reply": chatbot_reply})
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == '__main__':
    app.run(debug=True)

Frontend (HTML + CSS + JavaScript)

Create a file named index.html:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot Widget</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .chat-widget {
            width: 300px;
            height: 400px;
            border: 1px solid #ccc;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: white;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .chat-header {
            background-color: #0078d7;
            color: white;
            padding: 10px;
            text-align: center;
        }
        .chat-body {
            flex: 1;
            padding: 10px;
            overflow-y: auto;
            border-top: 1px solid #ccc;
        }
        .chat-input {
            display: flex;
            border-top: 1px solid #ccc;
        }
        .chat-input textarea {
            flex: 1;
            border: none;
            padding: 10px;
            resize: none;
        }
        .chat-input button {
            background-color: #0078d7;
            color: white;
            border: none;
            padding: 10px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="chat-widget">
        <div class="chat-header">Chat with us</div>
        <div class="chat-body" id="chatBody"></div>
        <div class="chat-input">
            <textarea id="userMessage" placeholder="Type your message..."></textarea>
            <button onclick="sendMessage()">Send</button>
        </div>
    </div>

    <script>
        async function sendMessage() {
            const userMessage = document.getElementById("userMessage").value;
            if (!userMessage.trim()) return;

            // Display user's message
            const chatBody = document.getElementById("chatBody");
            const userDiv = document.createElement("div");
            userDiv.textContent = "You: " + userMessage;
            chatBody.appendChild(userDiv);
            document.getElementById("userMessage").value = "";

            // Call backend API
            try {
                const response = await fetch('/chat', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ message: userMessage })
                });

                const data = await response.json();
                const botDiv = document.createElement("div");
                botDiv.textContent = "Bot: " + (data.reply || "Error in response");
                chatBody.appendChild(botDiv);
                chatBody.scrollTop = chatBody.scrollHeight;
            } catch (error) {
                const errorDiv = document.createElement("div");
                errorDiv.textContent = "Error: Unable to reach the server.";
                chatBody.appendChild(errorDiv);
            }
        }
    </script>
</body>
</html>

Steps to Run:

    Install Dependencies:

pip install flask openai

Set OpenAI API Key: Replace "your_openai_api_key" in the backend code with your actual OpenAI API key.
Run Flask Server:

    python app.py

    Host Frontend: Place the index.html file in the same directory or serve it through a local web server.
    Open in Browser: Access the chatbot widget on your website, connected to the Flask backend.

Features:

    User Engagement: Real-time interaction with visitors.
    Customizable Responses: Tailored to your FAQs and support needs.
    Scalable Backend: OpenAI's API ensures intelligent, context-aware replies.

Future Enhancements:

    Persistent Conversations: Store chat history using a database (e.g., SQLite, PostgreSQL).
    Multi-language Support: Enable the chatbot to understand and reply in multiple languages.
    Integration: Connect to CRM tools for customer tracking or analytics platforms to analyze usage.

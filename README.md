# VIRA-AI-<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vira AI - Your Intelligent Assistant</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #7E57C2;
            --primary-dark: #5E35B1;
            --secondary: #26A69A;
            --dark: #1A1A2E;
            --light: #F5F7FB;
            --gray: #E5E7EB;
            --text-dark: #1F2937;
            --text-light: #6B7280;
            --user-msg: #7E57C2;
            --ai-msg: #F0EBF8;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1A1A2E 0%, #16213E 100%);
            color: var(--light);
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
        }

        .header {
            background: rgba(26, 26, 46, 0.8);
            backdrop-filter: blur(10px);
            padding: 1rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            z-index: 100;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .logo-icon {
            font-size: 1.8rem;
            color: var(--primary);
        }

        .logo-text {
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .nav-links {
            display: flex;
            gap: 1.5rem;
        }

        .nav-link {
            color: var(--text-light);
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s;
        }

        .nav-link:hover {
            color: var(--primary);
        }

        .main-container {
            display: flex;
            flex: 1;
            overflow: hidden;
        }

        .sidebar {
            width: 260px;
            background: rgba(26, 26, 46, 0.7);
            backdrop-filter: blur(10px);
            padding: 1.5rem;
            border-right: 1px solid rgba(255, 255, 255, 0.1);
            overflow-y: auto;
            display: flex;
            flex-direction: column;
        }

        .new-chat-btn {
            background: linear-gradient(90deg, var(--primary), var(--primary-dark));
            color: white;
            border: none;
            border-radius: 8px;
            padding: 0.75rem 1rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            cursor: pointer;
            transition: transform 0.2s;
            margin-bottom: 1.5rem;
        }

        .new-chat-btn:hover {
            transform: translateY(-2px);
        }

        .history-title {
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: var(--text-light);
            margin-bottom: 1rem;
        }

        .chat-history {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .chat-item {
            padding: 0.75rem;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.3s;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--text-light);
        }

        .chat-item:hover {
            background: rgba(255, 255, 255, 0.1);
        }

        .chat-item i {
            font-size: 1rem;
        }

        .chat-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .chat-messages {
            flex: 1;
            padding: 2rem;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .message {
            max-width: 80%;
            padding: 1.25rem;
            border-radius: 12px;
            line-height: 1.6;
            animation: fadeIn 0.3s ease;
            position: relative;
        }

        .user-message {
            align-self: flex-end;
            background: var(--user-msg);
            color: white;
            border-bottom-right-radius: 4px;
        }

        .ai-message {
            align-self: flex-start;
            background: var(--ai-msg);
            color: var(--text-dark);
            border-bottom-left-radius: 4px;
        }

        .message-header {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.75rem;
            font-weight: 600;
        }

        .user-icon, .ai-icon {
            width: 28px;
            height: 28px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
        }

        .user-icon {
            background: rgba(255, 255, 255, 0.2);
        }

        .ai-icon {
            background: var(--primary);
            color: white;
        }

        .input-container {
            padding: 1.5rem;
            background: rgba(26, 26, 46, 0.7);
            backdrop-filter: blur(10px);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .input-box {
            display: flex;
            background: rgba(255, 255, 255, 0.08);
            border-radius: 12px;
            padding: 0.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #user-input {
            flex: 1;
            background: transparent;
            border: none;
            padding: 0.75rem 1rem;
            color: var(--light);
            font-size: 1rem;
            outline: none;
            resize: none;
            max-height: 150px;
            overflow-y: auto;
        }

        #send-button {
            background: linear-gradient(90deg, var(--primary), var(--primary-dark));
            color: white;
            border: none;
            width: 44px;
            height: 44px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            align-self: flex-end;
            transition: transform 0.2s;
        }

        #send-button:hover {
            transform: scale(1.05);
        }

        .input-options {
            display: flex;
            justify-content: space-between;
            margin-top: 0.75rem;
            color: var(--text-light);
            font-size: 0.9rem;
        }

        .examples {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1rem;
            margin-top: 2rem;
        }

        .example-card {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 1rem;
            cursor: pointer;
            transition: transform 0.2s, background 0.3s;
        }

        .example-card:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateY(-2px);
        }

        .example-title {
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--primary);
        }

        .typing-indicator {
            align-self: flex-start;
            background: var(--ai-msg);
            color: var(--text-dark);
            padding: 1.25rem;
            border-radius: 12px;
            margin-bottom: 1rem;
            display: none;
            border-bottom-left-radius: 4px;
        }

        .typing-indicator span {
            height: 8px;
            width: 8px;
            background: var(--primary);
            border-radius: 50%;
            display: inline-block;
            margin: 0 2px;
            opacity: 0.6;
            animation: bounce 1.3s infinite ease-in-out;
        }

        .typing-indicator span:nth-child(2) {
            animation-delay: 0.15s;
        }

        .typing-indicator span:nth-child(3) {
            animation-delay: 0.3s;
        }

        @keyframes bounce {
            0%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-6px); }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @media (max-width: 768px) {
            .sidebar {
                display: none;
            }
            
            .message {
                max-width: 90%;
            }
            
            .examples {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="logo">
            <div class="logo-icon"><i class="fas fa-robot"></i></div>
            <div class="logo-text">Vira AI</div>
        </div>
        <div class="nav-links">
            <a href="#" class="nav-link">Home</a>
            <a href="#" class="nav-link">Features</a>
            <a href="#" class="nav-link">Pricing</a>
            <a href="#" class="nav-link">About</a>
        </div>
    </header>

    <div class="main-container">
        <aside class="sidebar">
            <button class="new-chat-btn">
                <i class="fas fa-plus"></i> New Chat
            </button>
            
            <h3 class="history-title">Recent Conversations</h3>
            <div class="chat-history">
                <div class="chat-item">
                    <i class="fas fa-comment"></i>
                    <span>Python code help</span>
                </div>
                <div class="chat-item">
                    <i class="fas fa-comment"></i>
                    <span>Travel recommendations</span>
                </div>
                <div class="chat-item">
                    <i class="fas fa-comment"></i>
                    <span>AI explanations</span>
                </div>
                <div class="chat-item">
                    <i class="fas fa-comment"></i>
                    <span>Business plan advice</span>
                </div>
            </div>
        </aside>

        <main class="chat-container">
            <div class="chat-messages">
                <div class="message ai-message">
                    <div class="message-header">
                        <div class="ai-icon"><i class="fas fa-robot"></i></div>
                        <span>Vira AI</span>
                    </div>
                    Hello! I'm Vira AI, your intelligent assistant. How can I help you today?
                </div>
                
                <div class="examples">
                    <div class="example-card">
                        <div class="example-title">Explain concepts</div>
                        <div>Explain quantum computing in simple terms</div>
                    </div>
                    <div class="example-card">
                        <div class="example-title">Creative ideas</div>
                        <div>Give me ideas for a sci-fi novel</div>
                    </div>
                    <div class="example-card">
                        <div class="example-title">Code help</div>
                        <div>How to implement a neural network in Python?</div>
                    </div>
                    <div class="example-card">
                        <div class="example-title">Writing assistance</div>
                        <div>Help me write a professional email</div>
                    </div>
                </div>

                <div class="typing-indicator" id="typing-indicator">
                    <div class="message-header">
                        <div class="ai-icon"><i class="fas fa-robot"></i></div>
                        <span>Vira AI is typing</span>
                    </div>
                    <span></span>
                    <span></span>
                    <span></span>
                </div>
            </div>

            <div class="input-container">
                <div class="input-box">
                    <textarea id="user-input" placeholder="Message Vira AI..." rows="1"></textarea>
                    <button id="send-button">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </div>
                <div class="input-options">
                    <div>Vira AI can make mistakes. Consider checking important information.</div>
                    <div>© 2023 Vira AI</div>
                </div>
            </div>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const chatContainer = document.getElementById('chat-messages');
            const userInput = document.getElementById('user-input');
            const sendButton = document.getElementById('send-button');
            const typingIndicator = document.getElementById('typing-indicator');
            
            // Focus input on load
            userInput.focus();
            
            // Auto-resize textarea
            userInput.addEventListener('input', function() {
                this.style.height = 'auto';
                this.style.height = (this.scrollHeight) + 'px';
            });
            
            // Send message function
            function sendMessage() {
                const message = userInput.value.trim();
                if (message === '') return;
                
                // Add user message to chat
                addMessage(message, 'user');
                
                // Clear input and reset height
                userInput.value = '';
                userInput.style.height = 'auto';
                
                // Show typing indicator
                typingIndicator.style.display = 'block';
                chatContainer.scrollTop = chatContainer.scrollHeight;
                
                // Simulate AI response after a delay
                setTimeout(() => {
                    typingIndicator.style.display = 'none';
                    getAIResponse(message);
                }, 1500);
            }
            
            // Add message to chat
            function addMessage(text, sender) {
                const messageElement = document.createElement('div');
                messageElement.classList.add('message');
                messageElement.classList.add(sender + '-message');
                
                const messageHeader = document.createElement('div');
                messageHeader.classList.add('message-header');
                
                if (sender === 'user') {
                    messageHeader.innerHTML = `
                        <div class="user-icon"><i class="fas fa-user"></i></div>
                        <span>You</span>
                    `;
                } else {
                    messageHeader.innerHTML = `
                        <div class="ai-icon"><i class="fas fa-robot"></i></div>
                        <span>Vira AI</span>
                    `;
                }
                
                messageElement.appendChild(messageHeader);
                messageElement.appendChild(document.createTextNode(text));
                
                // Insert before typing indicator
                chatContainer.insertBefore(messageElement, typingIndicator);
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
            }
            
            // Get AI response (simulated for this example)
            function getAIResponse(userMessage) {
                // In a real implementation, you would call an API here
                // For demonstration, we'll use predefined responses
                
                const responses = [
                    "I understand what you're saying. How can I assist you further?",
                    "That's an interesting point. Could you tell me more about that?",
                    "I'm here to help with any questions you might have.",
                    "I'm designed to provide helpful, harmless, and honest responses.",
                    "Let me know if there's anything specific you'd like to know about.",
                    "I'm constantly learning and improving to better assist you."
                ];
                
                // Simple response logic based on keywords
                let response;
                
                if (userMessage.toLowerCase().includes('hello') || userMessage.toLowerCase().includes('hi')) {
                    response = "Hello there! How can I assist you today?";
                } else if (userMessage.toLowerCase().includes('help')) {
                    response = "I'd be happy to help! What do you need assistance with?";
                } else if (userMessage.toLowerCase().includes('thank')) {
                    response = "You're welcome! Is there anything else I can help with?";
                } else if (userMessage.toLowerCase().includes('name')) {
                    response = "I'm Vira AI, your intelligent assistant.";
                } else if (userMessage.toLowerCase().includes('weather')) {
                    response = "I don't have real-time weather data, but I can help you find weather information if you tell me your location.";
                } else {
                    // Random response from the list
                    response = responses[Math.floor(Math.random() * responses.length)];
                }
                
                addMessage(response, 'ai');
            }
            
            // Event listeners
            sendButton.addEventListener('click', sendMessage);
            
            userInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    sendMessage();
                }
            });
            
            // Example card click event
            document.querySelectorAll('.example-card').forEach(card => {
                card.addEventListener('click', function() {
                    userInput.value = this.querySelector('div:last-child').textContent;
                    userInput.focus();
                    userInput.dispatchEvent(new Event('input'));
                });
            });
        });
    </script>
</body>
</html>

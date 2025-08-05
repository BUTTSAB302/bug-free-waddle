# bug-free-waddle<!DOCTYPE html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Chat App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

```
    body {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .chat-container {
        width: 90%;
        max-width: 800px;
        height: 90vh;
        background: rgba(255, 255, 255, 0.95);
        backdrop-filter: blur(10px);
        border-radius: 20px;
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        display: flex;
        flex-direction: column;
        overflow: hidden;
    }

    .chat-header {
        background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        color: white;
        padding: 20px;
        text-align: center;
        position: relative;
    }

    .chat-header h1 {
        font-size: 24px;
        font-weight: 600;
    }

    .status-indicator {
        position: absolute;
        right: 20px;
        top: 50%;
        transform: translateY(-50%);
        display: flex;
        align-items: center;
        gap: 8px;
    }

    .status-dot {
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background: #4ade80;
        animation: pulse 2s infinite;
    }

    @keyframes pulse {
        0%, 100% { opacity: 1; }
        50% { opacity: 0.5; }
    }

    .chat-messages {
        flex: 1;
        padding: 20px;
        overflow-y: auto;
        display: flex;
        flex-direction: column;
        gap: 16px;
    }

    .message {
        display: flex;
        gap: 12px;
        max-width: 80%;
        animation: fadeInUp 0.3s ease-out;
    }

    @keyframes fadeInUp {
        from {
            opacity: 0;
            transform: translateY(20px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .message.user {
        align-self: flex-end;
        flex-direction: row-reverse;
    }

    .message.ai {
        align-self: flex-start;
    }

    .avatar {
        width: 40px;
        height: 40px;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: bold;
        flex-shrink: 0;
    }

    .user .avatar {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
    }

    .ai .avatar {
        background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        color: white;
    }

    .message-content {
        background: white;
        padding: 12px 16px;
        border-radius: 18px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        word-wrap: break-word;
    }

    .user .message-content {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
    }

    .timestamp {
        font-size: 11px;
        color: #666;
        margin-top: 4px;
    }

    .user .timestamp {
        color: rgba(255, 255, 255, 0.8);
    }

    .typing-indicator {
        display: none;
        align-items: center;
        gap: 12px;
        max-width: 80%;
        align-self: flex-start;
    }

    .typing-dots {
        background: white;
        padding: 12px 16px;
        border-radius: 18px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        display: flex;
        gap: 4px;
    }

    .typing-dot {
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background: #999;
        animation: typing 1.4s infinite;
    }

    .typing-dot:nth-child(2) {
        animation-delay: 0.2s;
    }

    .typing-dot:nth-child(3) {
        animation-delay: 0.4s;
    }

    @keyframes typing {
        0%, 60%, 100% {
            transform: translateY(0);
        }
        30% {
            transform: translateY(-10px);
        }
    }

    .chat-input {
        padding: 20px;
        background: rgba(247, 250, 252, 0.8);
        backdrop-filter: blur(10px);
        border-top: 1px solid rgba(0, 0, 0, 0.1);
    }

    .input-container {
        display: flex;
        gap: 12px;
        align-items: flex-end;
    }

    .input-field {
        flex: 1;
        min-height: 44px;
        max-height: 120px;
        padding: 12px 16px;
        border: 2px solid rgba(0, 0, 0, 0.1);
        border-radius: 22px;
        font-size: 16px;
        font-family: inherit;
        resize: none;
        outline: none;
        transition: all 0.3s ease;
        background: white;
    }

    .input-field:focus {
        border-color: #4facfe;
        box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
    }

    .send-button {
        width: 44px;
        height: 44px;
        border: none;
        border-radius: 50%;
        background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
        color: white;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 0.3s ease;
        flex-shrink: 0;
    }

    .send-button:hover {
        transform: scale(1.05);
        box-shadow: 0 4px 12px rgba(79, 172, 254, 0.4);
    }

    .send-button:disabled {
        opacity: 0.5;
        cursor: not-allowed;
        transform: none;
    }

    .welcome-message {
        text-align: center;
        color: #666;
        font-style: italic;
        padding: 40px;
    }

    /* Scrollbar styling */
    .chat-messages::-webkit-scrollbar {
        width: 6px;
    }

    .chat-messages::-webkit-scrollbar-track {
        background: transparent;
    }

    .chat-messages::-webkit-scrollbar-thumb {
        background: rgba(0, 0, 0, 0.2);
        border-radius: 3px;
    }

    .chat-messages::-webkit-scrollbar-thumb:hover {
        background: rgba(0, 0, 0, 0.3);
    }

    /* Mobile responsiveness */
    @media (max-width: 768px) {
        .chat-container {
            width: 95%;
            height: 95vh;
            border-radius: 15px;
        }

        .chat-header h1 {
            font-size: 20px;
        }

        .message {
            max-width: 90%;
        }

        .input-field {
            font-size: 16px; /* Prevents zoom on iOS */
        }
    }
</style>
```

</head>
<body>
    <div class="chat-container">
        <div class="chat-header">
            <h1>AI Chat Assistant</h1>
            <div class="status-indicator">
                <div class="status-dot"></div>
                <span>Online</span>
            </div>
        </div>

```
    <div class="chat-messages" id="chatMessages">
        <div class="welcome-message">
            👋 Welcome! I'm your AI assistant. How can I help you today?
        </div>
    </div>

    <div class="typing-indicator" id="typingIndicator">
        <div class="avatar">
            <span>🤖</span>
        </div>
        <div class="typing-dots">
            <div class="typing-dot"></div>
            <div class="typing-dot"></div>
            <div class="typing-dot"></div>
        </div>
    </div>

    <div class="chat-input">
        <div class="input-container">
            <textarea 
                class="input-field" 
                id="messageInput" 
                placeholder="Type your message here..."
                rows="1"
            ></textarea>
            <button class="send-button" id="sendButton">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M2 21L23 12L2 3V10L17 12L2 14V21Z" fill="currentColor"/>
                </svg>
            </button>
        </div>
    </div>
</div>

<script>
    class ChatApp {
        constructor() {
            this.messages = [];
            this.isTyping = false;
            
            this.chatMessages = document.getElementById('chatMessages');
            this.messageInput = document.getElementById('messageInput');
            this.sendButton = document.getElementById('sendButton');
            this.typingIndicator = document.getElementById('typingIndicator');
            
            this.initializeEventListeners();
            this.adjustTextareaHeight();
        }

        initializeEventListeners() {
            this.sendButton.addEventListener('click', () => this.sendMessage());
            this.messageInput.addEventListener('keypress', (e) => {
                if (e.key === 'Enter' && !e.shiftKey) {
                    e.preventDefault();
                    this.sendMessage();
                }
            });
            
            this.messageInput.addEventListener('input', () => {
                this.adjustTextareaHeight();
            });
        }

        adjustTextareaHeight() {
            this.messageInput.style.height = 'auto';
            this.messageInput.style.height = Math.min(this.messageInput.scrollHeight, 120) + 'px';
        }

        async sendMessage() {
            const messageText = this.messageInput.value.trim();
            if (!messageText || this.isTyping) return;

            // Add user message
            this.addMessage(messageText, 'user');
            this.messageInput.value = '';
            this.adjustTextareaHeight();
            
            // Show typing indicator
            this.showTyping();
            
            // Simulate AI response
            setTimeout(() => {
                this.hideTyping();
                const aiResponse = this.generateAIResponse(messageText);
                this.addMessage(aiResponse, 'ai');
            }, 1000 + Math.random() * 2000);
        }

        addMessage(text, sender) {
            const message = {
                text: text,
                sender: sender,
                timestamp: new Date()
            };
            
            this.messages.push(message);
            this.renderMessage(message);
            this.scrollToBottom();
        }

        renderMessage(message) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${message.sender}`;
            
            const avatar = document.createElement('div');
            avatar.className = 'avatar';
            avatar.textContent = message.sender === 'user' ? '👤' : '🤖';
            
            const content = document.createElement('div');
            content.className = 'message-content';
            content.textContent = message.text;
            
            const timestamp = document.createElement('div');
            timestamp.className = 'timestamp';
            timestamp.textContent = this.formatTime(message.timestamp);
            content.appendChild(timestamp);
            
            messageDiv.appendChild(avatar);
            messageDiv.appendChild(content);
            
            this.chatMessages.appendChild(messageDiv);
        }

        showTyping() {
            this.isTyping = true;
            this.typingIndicator.style.display = 'flex';
            this.sendButton.disabled = true;
            this.scrollToBottom();
        }

        hideTyping() {
            this.isTyping = false;
            this.typingIndicator.style.display = 'none';
            this.sendButton.disabled = false;
        }

        generateAIResponse(userMessage) {
            const responses = [
                "That's an interesting question! Let me think about that for a moment.",
                "I understand what you're asking. Here's my perspective on that topic.",
                "Great point! I'd be happy to help you with that.",
                "Thanks for sharing that with me. Here's what I think about it.",
                "That's a thoughtful question. Let me provide you with some insights.",
                "I appreciate you asking! Here's how I would approach that.",
                "Interesting! I can definitely help you explore that idea further.",
                "That's a complex topic. Let me break it down for you.",
                "I see what you're getting at. Here's my take on the situation.",
                "Good question! I think there are several ways to look at this."
            ];

            // Simple keyword-based responses
            const lowerMessage = userMessage.toLowerCase();
            
            if (lowerMessage.includes('hello') || lowerMessage.includes('hi') || lowerMessage.includes('hey')) {
                return "Hello! It's great to meet you. How are you doing today?";
            }
            
            if (lowerMessage.includes('how are you')) {
                return "I'm doing well, thank you for asking! I'm here and ready to help with whatever you need.";
            }
            
            if (lowerMessage.includes('weather')) {
                return "I don't have access to real-time weather data, but I'd recommend checking your local weather app or website for the most accurate forecast!";
            }
            
            if (lowerMessage.includes('help')) {
                return "I'm here to help! You can ask me questions, have a conversation, or just chat about whatever's on your mind.";
            }
            
            if (lowerMessage.includes('time')) {
                return `The current time is ${new Date().toLocaleTimeString()}. Is there anything specific you need help with regarding time?`;
            }
            
            if (lowerMessage.includes('name')) {
                return "I'm your AI chat assistant! You can call me whatever you'd like. What would you prefer to call me?";
            }
            
            if (lowerMessage.includes('thank') || lowerMessage.includes('thanks')) {
                return "You're very welcome! I'm happy I could help. Is there anything else you'd like to talk about?";
            }
            
            if (lowerMessage.includes('bye') || lowerMessage.includes('goodbye')) {
                return "Goodbye! It was nice chatting with you. Feel free to come back anytime!";
            }
            
            // Default to random response
            return responses[Math.floor(Math.random() * responses.length)];
        }

        formatTime(date) {
            return date.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        }

        scrollToBottom() {
            setTimeout(() => {
                this.chatMessages.scrollTop = this.chatMessages.scrollHeight;
            }, 100);
        }
    }

    // Initialize the chat app when the page loads
    document.addEventListener('DOMContentLoaded', () => {
        new ChatApp();
    });
</script>
```

</body>
</html>

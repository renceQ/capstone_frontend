<template>
  <div class="container mt-5">
    <h1 style="color:white">Warrens Chat Bot</h1>
    <div class="chat-box mt-3" ref="chatBox">
      <!-- Chat messages will be added here dynamically -->
    </div>
    <div class="form-group mt-3">
      <textarea class="form-control" rows="3" placeholder="Type your message here" v-model="message"></textarea>
    </div>
    <button type="button" class="btn btn-primary" @click="sendMessage">Send</button>
  </div>
</template>

<script>
import hljs from 'highlight.js/lib/highlight';
import 'highlight.js/styles/a11y-dark.css';

export default {
  data() {
    return {
      message: '',
    };
  },
  methods: {
    highlightAll() {
      this.$refs.chatBox.querySelectorAll("pre code").forEach(block => {
        hljs.highlightBlock(block);
      });
    },
    addMessage(message, isUserMessage) {
      const messageDiv = document.createElement("div");
      messageDiv.classList.add("mt-3", "p-3", "rounded");

      if (isUserMessage) {
        messageDiv.classList.add("user-message");
      } else {
        messageDiv.classList.add("bot-message");
      }

      messageDiv.innerHTML = `
        <img src="${require('../../public/img/gcash.png')}" class="user-icon"><p>${message}</p>
      `;

      this.$refs.chatBox.appendChild(messageDiv);
      this.$refs.chatBox.scrollTop = this.$refs.chatBox.scrollHeight;
    },
    sendMessage() {
  const message = this.message.trim();

  if (message !== "") {
    this.addMessage(message, true);

    // Replace 'YOUR_API_KEY' with your actual OpenAI GPT API key
    const apiKey = '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';
    const apiUrl = 'https://api.openai.com/v1/engines/davinci-codex/completions';

    fetch(apiUrl, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${apiKey}`,
      },
      body: JSON.stringify({
        prompt: message,
        max_tokens: 100,
      }),
    })
      .then(response => response.json())
      .then(data => {
        this.message = "";
        const content = data.choices[0].text.trim();
        this.addMessage(content, false);
      })
      .catch(error => console.error(error));
  }
},

  },
  mounted() {
    setInterval(this.highlightAll, 1000);
  },
};
</script>

<style>
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.4;
  background-color: rgb(7, 7, 7);
  margin: 0;
  padding: 0;
}

.chat-box {
  height: 350px;
  overflow: auto;
  padding: 10px;
}

.chat-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.chat-message {
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}

.user-message {
  background-color: #272a2b;
  color: #fff;
  font-size: 20px;
}

.bot-message {
  background-color: #484848;
  color: white;
  font-size: 20px;
}

.message-text pre code {
  font-size: 14px;
  white-space: pre-wrap;
}

.user-icon {
  font-size: 20px;
  margin-right: 10px;
  border-radius: 50%;
  width: 50px;
  height: 50px;
}

.bot-icon {
  font-size: 20px;
  margin-right: 10px;
  border-radius: 50%;
  width: 50px;
  height: 50px;
}
</style>

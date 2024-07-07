---
title: "Interactive Message Generator"
date: 2024-07-06 12:00:00 -0500
categories: [Programming, Fun]
tags: [python, interactive-script, message-generator]
---

# Interactive Message Generator

Today, we're exploring a fun and interactive message generator that I've developed. This Python script creates personalized messages with a cool typing effect, making it perfect for romantic notes, friendly messages, or custom greetings!

## Try It Out!

<div id="message-generator">
  <label for="recipient-name">Recipient's Name:</label>
  <input type="text" id="recipient-name" placeholder="Enter name">
  <br><br>
  <label for="message-type">Message Type:</label>
  <select id="message-type">
    <option value="romantic">Romantic</option>
    <option value="friendly">Friendly</option>
    <option value="custom">Custom</option>
  </select>
  <br><br>
  <div id="custom-message-container" style="display: none;">
    <label for="custom-message">Custom Message:</label>
    <textarea id="custom-message" rows="4" cols="50"></textarea>
  </div>
  <br>
  <button onclick="generateMessage()">Generate Message</button>
  <div id="message-output"></div>
</div>

<script>
function generateMessage() {
  const name = document.getElementById('recipient-name').value;
  const messageType = document.getElementById('message-type').value;
  const customMessage = document.getElementById('custom-message').value;

  fetch('http://github.karetechsolutions.com:5550/generate', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      name: name,
      type: messageType,
      custom_message: customMessage
    }),
  })
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    return response.json();
  })
  .then(data => {
    const outputDiv = document.getElementById('message-output');
    outputDiv.innerHTML = '';
    let i = 0;
    function typeWriter() {
      if (i < data.message.length) {
        outputDiv.innerHTML += data.message.charAt(i) === '\n' ? '<br>' : data.message.charAt(i);
        i++;
        setTimeout(typeWriter, 50);
      }
    }
    typeWriter();
  })
  .catch((error) => {
    console.error('Error:', error);
    document.getElementById('message-output').innerHTML = `An error occurred: ${error.message}. Please try again.`;
  });
}

document.getElementById('message-type').addEventListener('change', function() {
  const customMessageContainer = document.getElementById('custom-message-container');
  customMessageContainer.style.display = this.value === 'custom' ? 'block' : 'none';
});
</script>

<style>
#message-generator {
  background-color: #f0f0f0;
  border: 1px solid #ddd;
  padding: 20px;
  margin: 20px 0;
  border-radius: 5px;
}

#message-output {
  white-space: pre-wrap;
  font-family: monospace;
  margin-top: 20px;
  background-color: white;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
}
</style>

## How It Works

The script performs the following steps:

1. Takes the recipient's name as input.
2. Allows you to choose between pre-defined message templates (romantic or friendly) or a custom message.
3. Generates the message based on your choice.
4. Displays the message with a cool typing effect.

## Key Features

- Choice of romantic or friendly pre-defined messages
- Option to create a custom message
- Simulated typing effect for a more interactive display

[Rest of your post content...]
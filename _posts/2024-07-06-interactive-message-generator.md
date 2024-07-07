<script>
function generateMessage() {
  const name = document.getElementById('recipient-name').value;
  const messageType = document.getElementById('message-type').value;
  const customMessage = document.getElementById('custom-message').value;

  fetch('http://github.karetechsolutions.com/generate', {
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
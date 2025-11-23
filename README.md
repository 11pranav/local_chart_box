
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Simple Chat</title>
  <style>
    body { font-family: sans-serif; margin: 2em; }
    #messages { border: 1px solid #ccc; padding: 1em; height: 200px; overflow-y: scroll; }
    form { margin-top: 1em; }
  </style>
</head>
<body>
  <h1>Chat Room</h1>
  <div id="messages"></div>

  <form id="chatForm" method="POST" action="/send">
    <input type="text" name="user" placeholder="Your name" required>
    <input type="text" name="message" placeholder="Message" required>
    <button type="submit">Send</button>
  </form>

  <script>
    const messagesDiv = document.getElementById('messages');

    async function loadMessages() {
      const res = await fetch('/messages');
      const msgs = await res.json();
      messagesDiv.innerHTML = msgs.map(m => `<b>${m.user}</b>: ${m.message}`).join('<br>');
      messagesDiv.scrollTop = messagesDiv.scrollHeight;
    }

    setInterval(loadMessages, 1000); // Poll every second
    loadMessages();
  </script>
</body>
</html># local_chart_box

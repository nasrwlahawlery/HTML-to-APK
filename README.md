<!DOCTYPE html>
<html lang="ku">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>kurd Medya Lave</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(to right, #00c6ff, #0072ff);
      margin: 0;
      direction: rtl;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 10px;
    }

    .chat-container {
      background: white;
      border-radius: 24px;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.25);
      display: flex;
      flex-direction: column;
      height: 90vh;
      max-height: 700px;
      width: 100%;
      max-width: 400px;
      overflow: hidden;
    }

    .chat-header {
      background: linear-gradient(to right, #6a11cb, #2575fc);
      color: white;
      padding: 1rem;
      text-align: center;
      font-size: 1.4rem;
      font-weight: bold;
      user-select: none;
    }

    .chat-messages {
      flex: 1;
      padding: 1rem;
      overflow-y: auto;
      background: #f8f9fd;
      scroll-behavior: smooth;
    }

    .message {
      margin: 0.5rem 0;
      padding: 0.8rem 1.2rem;
      border-radius: 18px;
      max-width: 85%;
      word-wrap: break-word;
      line-height: 1.5;
      font-size: 1rem;
      user-select: text;
    }

    .user-message {
      background: #d1d8e0;
      align-self: flex-end;
    }

    .bot-message {
      background: #74b9ff;
      align-self: flex-start;
      color: #fff;
    }

    .chat-input {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      border-top: 1px solid #dfe6e9;
      padding: 0.5rem;
      background: #ecf0f1;
      gap: 6px;
    }

    .chat-input input[type="text"] {
      flex: 1 1 auto;
      padding: 0.8rem;
      border: none;
      border-radius: 12px;
      font-size: 1rem;
      outline: none;
      min-width: 0;
    }

    .chat-input button {
      background: #0984e3;
      color: white;
      border: none;
      padding: 0.8rem 1.2rem;
      border-radius: 12px;
      font-size: 1rem;
      cursor: pointer;
      white-space: nowrap;
      flex-shrink: 0;
    }

    .chat-input button:hover {
      background: #0066cc;
    }

    .chat-input input[type="file"] {
      display: none;
    }

    .file-label {
      background: #6c5ce7;
      color: white;
      padding: 0.6rem 1rem;
      font-size: 0.85rem;
      cursor: pointer;
      border-radius: 10px;
      white-space: nowrap;
      flex-shrink: 0;
    }

    .file-label:hover {
      background: #4834d4;
    }

    img, video {
      max-width: 100%;
      border-radius: 14px;
      margin-top: 5px;
      display: block;
    }

    .emoji-bar {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      padding: 0.5rem 1rem;
      background: #dfe6e9;
      border-top: 1px solid #ccc;
      justify-content: center;
    }

    .emoji-bar span {
      cursor: pointer;
      font-size: 1.5rem;
      transition: transform 0.2s ease;
    }

    .emoji-bar span:hover {
      transform: scale(1.3);
    }

    .reactions {
      display: flex;
      gap: 10px;
      margin-top: 6px;
      align-items: center;
    }

    .reaction-button {
      background: #dfe6e9;
      border: none;
      padding: 4px 10px;
      border-radius: 12px;
      cursor: pointer;
      font-size: 0.85rem;
    }

    .reaction-button:hover {
      background: #b2bec3;
    }

    /* Responsive adjustments */
    @media (max-width: 480px) {
      .chat-container {
        height: 100vh;
        border-radius: 0;
        max-width: 100%;
      }
      .chat-input input[type="text"] {
        font-size: 0.9rem;
      }
      .chat-header {
        font-size: 1.2rem;
        padding: 0.8rem;
      }
      .message {
        font-size: 0.9rem;
        padding: 0.6rem 1rem;
      }
      .chat-input button, .file-label {
        font-size: 0.9rem;
        padding: 0.6rem 1rem;
      }
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-header">💬 kurd Medya Lave</div>
    <div class="chat-messages" id="messages"></div>
    <div class="emoji-bar" aria-label="Emojis">
      <span role="button" tabindex="0" onclick="insertEmoji('😊')">😊</span>
      <span role="button" tabindex="0" onclick="insertEmoji('😂')">😂</span>
      <span role="button" tabindex="0" onclick="insertEmoji('🥰')">🥰</span>
      <span role="button" tabindex="0" onclick="insertEmoji('👍')">👍</span>
      <span role="button" tabindex="0" onclick="insertEmoji('🔥')">🔥</span>
      <span role="button" tabindex="0" onclick="insertEmoji('❤️')">❤️</span>
      <span role="button" tabindex="0" onclick="insertEmoji('🤔')">🤔</span>
      <span role="button" tabindex="0" onclick="insertEmoji('😢')">😢</span>
      <span role="button" tabindex="0" onclick="insertEmoji('👏')">👏</span>
    </div>
    <div class="chat-input">
      <label for="fileInput" class="file-label" aria-label="Send Image or Video">📎 وێنە/ڤیدیۆ</label>
      <input type="file" id="fileInput" accept="image/*,video/*" onchange="sendFile(event)" />
      <button onclick="openCamera()" aria-label="Open Camera">📷 کامێرا</button>
      <input type="text" id="userInput" placeholder="پرسیارەکەت بنووسە..." aria-label="Message input" />
      <button onclick="sendMessage()" aria-label="Send message">📨 ناردن</button>
    </div>
  </div>

  <script>
    const qa = {
      "سڵاو": "سڵاو، چۆنی؟ 😊",
      "HTML چییە؟": "زمانێکە بۆ دروستکردنی پەڕەی وێب 📄.",
      "کەی نەورۆزە؟": "لە 21ی ئەدار 🎉.",
      "ناوت چییە؟": "من چات بۆتێکم 🤖!",
      "کوردستان لە کوێیە؟": "لە ناوچەی ڕۆژهەڵاتی ناوەڕاست 🗺️.",
      "ناوی پایتەختی کوردستان؟": "هەولێر 🏙️."
    };

    const system = [
      "📌 ئەم چات بۆتە وەلامە کوردییەکان داتەوێت.",
      "💡 تۆ دەتوانیت پرسیار بنووسیت و وەلام وەربگریت.",
      "📎 دەتوانیت وێنە و ڤیدیۆ نێریت بۆ پیشاندانیەوە.",
      "📷 دەتوانیت بە کامێراش وێنە بگریت و بنێریت."
    ];

    window.onload = () => {
      const messages = document.getElementById('messages');
      system.forEach(line => {
        const intro = document.createElement('div');
        intro.className = 'message bot-message';
        intro.textContent = line;
        messages.appendChild(intro);
      });
    };

    function sendMessage() {
      const input = document.getElementById('userInput');
      const userText = input.value.trim();
      if (!userText) return;

      const messages = document.getElementById('messages');

      const userMsg = document.createElement('div');
      userMsg.className = 'message user-message';
      userMsg.textContent = userText;
      messages.appendChild(userMsg);

      const answer = qa[userText] || "ببورە، وەلامەکە نەدۆزرایەوە. 🤷‍♂️";
      const botMsg = document.createElement('div');
      botMsg.className = 'message bot-message';
      botMsg.textContent = answer;
      messages.appendChild(botMsg);

      messages.scrollTop = messages.scrollHeight;
      input.value = '';
    }

    function sendFile(event) {
      const file = event.target.files[0];
      if (!file) return;

      const messages = document.getElementById('messages');
      const fileMsg = document.createElement('div');
      fileMsg.className = 'message user-message';

      if (file.type.startsWith('image/')) {
        const img = document.createElement('img');
        img.src = URL.createObjectURL(file);
        fileMsg.appendChild(img);
      } else if (file.type.startsWith('video/')) {
        const video = document.createElement('video');
        video.src = URL.createObjectURL(file);
        video.controls = true;
        fileMsg.appendChild(video);
      } else {
        fileMsg.textContent = "پەڕگەکە پشتیوانی ناکرێت.";
      }

      const reactions = document.createElement('div');
      reactions.className = 'reactions';
      reactions.innerHTML = `
        <button class="reaction-button">❤️ Like</button>
        <button class="reaction-button">💬 Comment</button>
      `;
      fileMsg.appendChild(reactions);

      messages.appendChild(fileMsg);
      messages.scrollTop = messages.scrollHeight;
    }

    function openCamera() {
      const input = document.createElement('input');
      input.type = 'file';
      input.accept = 'image/*';
      input.capture = 'environment';
      input.onchange = sendFile;
      input.click();
    }

    function insertEmoji(emoji) {
      const input = document.getElementById('userInput');
      input.value += emoji;
      input.focus();
    }
  </script>
</body>
</html>


<!DOCTYPE html>
<html>
<head>
  <title>Простой Чат-бот</title>

  <style>
  .ICON{
   position: absolute;
      top: -6%;
      left: 47%;
      width:5%;
      margin: 50px auto;
      border: 10px solid rgba(255,255,255, 0,8);
      border-radius: 200px;
  }

    .text {
	 display: flex;
      justify-content: center;
      align-items: center;

      margin: 0;
      font-family: sans-serif;
      font-size: 4em;
      color: #800080; /* Начальный фиолетовый цвет */
      animation: color-shift 3s linear infinite;
    }

    @keyframes color-shift {
      0% {
        color: #800080; /* Фиолетовый */
      }
      50% {
        color: #0000ff; /* Голубой */
      }
      100% {
        color: #800080; /* Фиолетовый */
      }
    }
  </style>
</head>
<body>




  <style>
body{
background-position: fixed;
  background-image: url('C:/операционая система ZIRO/Системные файли/botbg.png');
}

    .chat-container {
	background: linear-gradient(135deg,rgba(225,225,225 0,1),rgba(225,225,0));
	backdrop-filter:blur(20px);
	-webkit-backdrop-filter:blur(10px);

      display: flex;
      flex-direction: column;
      width: 90%;
      margin: 50px auto;
      border: 10px solid rgba(255,255,255, 0,8);
	  box-shadow: 0 8px 32px 0 rgba(0,0,0,0.37);
      padding: 10px;
      border-radius: 10px;
    }

    .chat-message {

      padding: 10px;
      margin-bottom: 10px;
      border-radius: 5px;
    }

    .user-message {
     background-color: #7b68ee;
      color: #ffffff;
      position: relative;
    }

    .bot-message {
	  background-color:#2F4F4F;
      color: #ffffff;

    }

    .typing-indicator {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      display: inline-block;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background-color: #fff;
      animation: typing 1s linear infinite;
    }

    @keyframes typing {
      0% {
        opacity: 1;
        transform: translate(-50%, -50%) scale(1);
      }
      50% {
        opacity: 0.5;
        transform: translate(-50%, -50%) scale(1.2);
      }
      100% {
        opacity: 1;
        transform: translate(-50%, -50%) scale(1);
      }
    }

    input[type="text"] {

       position: fixed; /* Фиксируем контейнер на экране */
      bottom: 20px; /* Отступ от нижнего края */
      left: 70px; /* Центрирование по горизонтали */
      transform: translateX(-50%); /* Дополнительное центрирование */
      background-color: #fff;
      padding: 10px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); /* Добавляем тень */
      width: 30%; /* Ширина контейнера */
      width: 90px; /* Максимальная ширина */
    }

    button {
	img-src = "https://cdn-icons-png.flaticon.com/512/2111/2111644.png";
	 position: fixed; /* Фиксируем контейнер на экране */
      bottom: 20px; /* Отступ от нижнего края */
    left: 165px; /* Центрирование по горизонтали */
      transform: translateX(-50%); /* Дополнительное центрирование */
      background-color: #fff;
      padding: 10px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); /* Добавляем тень */
      width:80px; /* Ширина контейнера */
      max-width: 500px; /* Максимальная ширина */
      padding: 10px 20px;
      margin-top: 10px;
      border: none;
      background-color: #7b68ee;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>


  <script>
    const chatMessages = document.getElementById('chat-messages');
    const userInput = document.getElementById('user-input');

    function sendMessage() {
      const message = userInput.value;
      if (message.trim() !== '') {
        // Display user message
        displayMessage(message, 'user-message');
        userInput.value = '';

        // Simulate bot typing
        const botMessage = "Bot: " + generateBotResponse(message);
        typeMessage(botMessage, 'bot-message');
      }
    }

    function displayMessage(message, className) {
      const messageElement = document.createElement('div');
      messageElement.classList.add('chat-message', className);
      messageElement.textContent = message;
      chatMessages.appendChild(messageElement);
    }

    function generateBotResponse(message) {
      // Replace with your actual bot logic
      return "This is a response to your message: " + message;
    }

    function typeMessage(message, className) {
      const messageElement = document.createElement('div');
      messageElement.classList.add('chat-message', className);
      messageElement.textContent = ''; //  &lt;-- Добавлено, чтобы текст начинался пустым

      // Add typing indicator
      const typingIndicator = document.createElement('span');
      typingIndicator.classList.add('typing-indicator');
      messageElement.appendChild(typingIndicator);

      chatMessages.appendChild(messageElement);

      let i = 0;
      const interval = setInterval(() => {
        if (i < message.length) {
          messageElement.textContent += message.charAt(i);
          i++;
        } else {
          clearInterval(interval);
          // Remove typing indicator
          typingIndicator.remove();
        }
      }, 50);
    }
  </script>
</head>

  <div class="chat-container">


  </div>

  <input type="text" id="message-input" placeholder="Введите сообщение...">
  <button onclick="sendMessage()">Отправить</button>

  <script>
    const chatContainer = document.querySelector('.chat-container');
    const messageInput = document.getElementById('message-input');

    function sendMessage() {
      const message = messageInput.value.trim();
      if (message !== '') {
        // Добавляем сообщение пользователя
        const userMessage = document.createElement('div');
        userMessage.classList.add('chat-message', 'user-message');
        userMessage.textContent = message;
        chatContainer.appendChild(userMessage);

        // Отвечаем ботом
        const botResponse = getBotResponse(message);
        const botMessage = document.createElement('div');
        botMessage.classList.add('chat-message', 'bot-message');
        botMessage.textContent = botResponse;
        chatContainer.appendChild(botMessage);

        messageInput.value = ''; // Очищаем поле ввода
      }
    }

    // Массив для хранения пар вопрос-ответ ДЛЯ КАЖДОГО СЛОВА ОТДЕЛНЫЙ ВИД С  ОШИБКАМИ
	//ПРИВЕТ
   const questionsAndAnswers = [
  {
    question: "привет джарвис",
    answers: [
      "Здравствуйте сэр! 👋 Как у вас дела?",
      "Здравствуйте ! 👋 Чем могу помочь?",
      "Приветствую сэр! 👋"
    ]

},
{
  question: "список задач",
  answers: [
    " Вот ваш список сэр: 1)убраться в комнате 2)Учить програмирование 3)Поченит люстру"
  ]

},
{
  question: "список задач на сегодня",
  answers: [
    " Вот ваш список сэр: 1)убраться в комнате 2)Учить програмирование 3)Поченит люстру"
  ]

},
{
  question: "как у тебя дела?",
  answers: [
    "О здравствуйте сэр! Всё хорошо чем могу помочь?",
    "Здравствуйте сэр!  Чем могу помочь ?",
    "Всё прелесно сэр! ",
    "Пока что хорошо сэр! Чем то могу помочь ?"
  ]

},

{
  question: "привет",
  answers: [
    "О здравствуйте сэр!  Как ваши дела?",
    "Здравствуйте сэр! Чем могу помочь ?",
    "Приветствую вас сэр ! "
  ]

},
{
  question: "джарвис",
  answers: [
    "О здравствуйте сэр! Как ваши дела?",
    "Здравствуйте сэр! Чем могу помочь ?",
    "Приветствую вас сэр ! 👋"
  ]

}
];
function getBotResponse(message) {
  const normalizedMessage = message.toLowerCase();
for (const item of questionsAndAnswers) {
    if (item.question.toLowerCase() == normalizedMessage) {
      const randomIndex = Math.floor(Math.random() * item.answers.length);
      return item.answers[randomIndex];
    }
  }
return "не понимаю. Попробуй перефразировать. 😕";




}


  </script>

</body>
</html>

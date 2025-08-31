<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>ChatBot de Suporte ao Colaborador</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #007bff; /* fundo azul */
    }
    .chat-container {
      width: 400px;
      max-width: 90%;
      height: 600px;
      background: #ffffff; /* fundo branco do chat */
      border-radius: 10px;
      box-shadow: 0 0 15px rgba(0,0,0,0.3);
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }
    .chat-box {
      flex: 1;
      padding: 15px;
      overflow-y: auto;
      background: #e6f0ff; /* azul claro */
    }
    .chat-message {
      margin: 5px 0;
      padding: 10px;
      border-radius: 12px;
      max-width: 80%;
      word-wrap: break-word;
    }
    .chat-message.user {
      background: #007bff;
      color: white;
      align-self: flex-end;
    }
    .chat-message.bot {
      background: #ffffff;
      color: #333;
      align-self: flex-start;
    }
    .chat-input {
      display: flex;
      border-top: 1px solid #ddd;
    }
    .chat-input input {
      flex: 1;
      padding: 10px;
      border: none;
      outline: none;
      font-size: 16px;
    }
    .chat-input button {
      padding: 10px 20px;
      border: none;
      background: #0056b3;
      color: white;
      cursor: pointer;
      font-size: 16px;
    }
    .chat-input button:hover {
      background: #003f7f;
    }
    a {
      color: #007bff;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
    iframe.pdf-frame {
      width: 100%;
      height: 400px;
      border: none;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div id="chatBox" class="chat-box"></div>
    <div class="chat-input">
      <input id="userInput" type="text" placeholder="Digite sua dúvida...">
      <button id="sendButton">Enviar</button>
    </div>
  </div>

  <script>
    function addMessage(text, sender) {
      let chatBox = document.getElementById("chatBox");
      let messageElement = document.createElement("div");
      messageElement.className = "chat-message " + sender;
      messageElement.innerHTML = text;
      chatBox.appendChild(messageElement);
      chatBox.scrollTop = chatBox.scrollHeight;
    }

    function sendMessage() {
      let input = document.getElementById("userInput");
      let message = input.value.trim();
      if (message === "") return;

      addMessage("Você: " + input.value, "user");
      input.value = "";

      let resposta = "";
      let msg = message.toLowerCase();

      if (msg.includes("elegibilidade") || msg.includes("quem tem direito") || msg === "1" || msg === "1.") {
        resposta = "<b>Elegibilidade</b><br>" +
                   "<b>Mensalistas/Horistas:</b> O benefício é estendido a titulares e seus dependentes (cônjuge, companheiro(a), filhos e enteados), com comprovação.<br>" +
                   "Filhos entre 21 e 24 anos devem apresentar comprovante de matrícula em universidade.<br>" +
                   "<b>Instrutor e Professor Horista:</b> Apenas titulares têm direito ao auxílio.";

      } else if (msg.includes("prazo") || msg.includes("procedimento") || msg.includes("como solicitar") || msg === "2" || msg === "2.") {
        resposta = "<b>Prazos e Procedimentos</b><br>" +
                   "A solicitação pode ser feita a partir do primeiro mês de admissão, após 15 dias de trabalho.<br>" +
                   "A requisição de reembolso deve ser realizada entre os dias 1 e 15 de cada mês.<br><br>" +
                   "Portais de acesso:<br>" +
                   "• <a href='https://portalrh.sesc-ce.com.br/corpore.net/Login.aspx' target='_blank'>Colaboradores SESC - Portal Meu RH</a><br>" +
                   "• <a href='https://portalrh.ce.senac.br/Corpore.Net/Login.aspx' target='_blank'>Colaboradores SENAC - Portal Meu RH</a><br><br>" +
                   "Documentos: boleto, comprovante de pagamento e demonstrativo com identificação dos beneficiários.<br><br>" +
                   "Veja o passo a passo completo abaixo:<br>" +
                   "<iframe class='pdf-frame' src='https://drive.google.com/file/d/1AF4CmTEHWT2j3_eYVDHLxYQup2kTZPJW/preview'></iframe>";

      } else if (msg.includes("plano unimed") || msg.includes("plano hapvida") || msg.includes("adesão") || msg.includes("contratar plano") || msg === "3" || msg === "3.") {
        resposta = "<b>Plano UNIMED / HAPVIDA</b><br>Para adesão, entre em contato com a Fecomercio: (85) 98728-8314 ou (85) 98883-4292.";

      } else if (msg.includes("valores") || msg.includes("reembolso") || msg.includes("cargo") || msg === "4" || msg === "4.") {
        resposta = "<b>Valores de Reembolso por Cargo</b><br>" +
                   "• <b>Operacional I e II:</b> Até R$ 377,62 (empregado) e R$ 125,87 (dependente).<br>" +
                   "• <b>Professor (mensalista):</b> Até R$ 363,32 / R$ 121,11<br>" +
                   "• <b>Professor/Instrutor (horista):</b> Até R$ 217,99 / sem auxílio dependente.<br>" +
                   "• <b>Técnico I, II, III, IV/Especialista e V:</b> Até R$ 220,19 / R$ 73,40.<br>" +
                   "• <b>Coordenação Corporativa e Especialista II/Tático I:</b> Até R$ 138,63 / R$ 46,21.<br>" +
                   "• <b>Piso Salarial I e II, Especialista III/Tático II, Especialista IV/Tático III e Gerência Corporativa SENAC/SESC:</b> Até R$ 132,82 / R$ 44,28.<br>" +
                   "• <b>Especialista V, Estratégico I e II:</b> Até R$ 99,62 / R$ 33,21.";

      } else if (msg.includes("obrigado") || msg.includes("obrigada") || msg.includes("valeu")) {
        resposta = "De nada! Se tiver mais alguma dúvida, é só perguntar.";

      } else if (msg.includes("tchau") || msg.includes("até logo") || msg.includes("fui")) {
        resposta = "Até logo! Se precisar, estarei aqui para ajudar.";

      } else {
        resposta = "Desculpe, não entendi sua dúvida.<br>👉 Se precisar de ajuda mais detalhada, entre em contato com a CAP: <a href='mailto:cap@senac.ce.br'>cap@senac.ce.br</a>";
      }

      setTimeout(() => addMessage("ChatBot: " + resposta, "bot"), 400);
    }

    document.getElementById("sendButton").addEventListener("click", sendMessage);
    document.getElementById("userInput").addEventListener("keypress", function(event) {
      if (event.key === "Enter") sendMessage();
    });

    window.onload = function() {
      addMessage("ChatBot: Olá! 👋 Sou um assistente da CAP. Posso responder sobre:<br>" +
                 "1. Elegibilidade<br>2. Prazos e Procedimentos<br>3. Plano UNIMED / HAPVIDA<br>4. Valores de Reembolso<br><br>" +
                 "<i>Se sua dúvida não for resolvida aqui, envie e-mail: <a href='mailto:cap@senac.ce.br'>cap@senac.ce.br</a></i>", "bot");
    };
  </script>
</body>
</html>

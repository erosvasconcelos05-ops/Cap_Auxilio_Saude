<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>ChatBot de Suporte ao Colaborador</title>
  <style>
    body { font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; background: #f2f2f2; }
    .chat-container { width: 400px; max-width: 90%; height: 600px; background: white; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); display: flex; flex-direction: column; }
    .chat-box { flex: 1; padding: 10px; overflow-y: auto; border-bottom: 1px solid #ddd; }
    .chat-message { margin: 10px 0; padding: 8px 12px; border-radius: 15px; max-width: 80%; word-wrap: break-word; }
    .user { background-color: #007bff; color: white; margin-left: auto; text-align: right; }
    .bot { background-color: #e9ecef; color: #333; margin-right: auto; text-align: left; }
    .input-box { display: flex; border-top: 1px solid #ddd; }
    input { flex: 1; padding: 15px; border: none; outline: none; border-radius: 0 0 0 10px; font-size: 16px; }
    button { padding: 15px 20px; border: none; background: #007bff; color: white; cursor: pointer; border-radius: 0 0 10px 0; font-size: 16px; transition: background-color 0.3s ease; }
    button:hover { background: #0056b3; }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-box" id="chatBox"></div>
    <div class="input-box">
      <input type="text" id="userInput" placeholder="Digite sua mensagem...">
      <button id="sendButton">Enviar</button>
    </div>
  </div>

  <script>
    function sendMessage() {
      let input = document.getElementById("userInput");
      let message = input.value.trim();
      if (message === "") return;

      addMessage("Você: " + message, "user");
      input.value = "";

      let resposta = "";
      let msg = message.toLowerCase();

      if (msg.includes("elegibilidade") || msg.includes("quem tem direito") || msg === "1" || msg === "1.") {
    resposta = "<b>Elegibilidade</b><br><b>Mensalistas/Horistas:</b> O benefício é estendido a titulares e seus dependentes (cônjuge, companheiro(a), filhos e enteados), com a devida comprovação. Filhos entre 21 e 24 anos devem apresentar comprovante de matrícula em universidade.<br><b>Instrutor e Professor Horista:</b> Apenas os titulares têm direito ao auxílio. Dependentes não são elegíveis.";
} else if (msg.includes("prazo") || msg.includes("procedimento") || msg.includes("como solicitar") || msg === "2" || msg === "2.") {
    resposta = "<b>Prazos e Procedimentos</b><br>A solicitação pode ser feita a partir do primeiro mês de admissão, após 15 dias de trabalho.<br>A requisição de reembolso deve ser realizada entre os dias 1 e 15 de cada mês, através do <a href='https://portalrh.sesc-ce.com.br/corpore.net/Main.aspx?ShowMode=2&SelectedMenuIDKey=' target='_blank'>Portal RM</a>.<br>É necessário enviar os seguintes documentos: boleto, comprovante de pagamento e um demonstrativo com a identificação dos beneficiários.";
} else if (msg.includes("plano unimed") || msg.includes("plano hapvida") || msg.includes("adesão") || msg.includes("contratar plano") || msg === "3" || msg === "3.") {
    resposta = "<b>Plano UNIMED / HAPVIDA</b><br>Para adesão ao plano, entre em contato com a Fecomercio pelos números:<br>(85) 98728-8314 ou (85) 98883-4292.";
} else if (msg.includes("valores") || msg.includes("reembolso") || msg.includes("cargo") || msg === "4" || msg === "4.") {
    resposta = "<b>Valores de Reembolso por Cargo</b><br>• Operacional I e II: Até R$ 377,62 (empregado) e R$ 125,87 (dependente).<br>• Professor (mensalista): Até R$ 363,32 (empregado) e R$ 121,11 (dependente).<br>• Professor/Instrutor (horista): Até R$ 217,99 (empregado) e sem auxílio para dependente.<br>• Técnico I, II, III, IV/Especialista e V: Até R$ 220,19 (empregado) e R$ 73,40 (dependente).<br>• Piso Salarial I e II, Especialista III/Tático II, Especialista IV/Tático III e Gerência Corporativa SENAC/SESC: Até R$ 132,82 (empregado) e R$ 44,28 (dependente).<br>• Especialista V, Estratégico I e II: Até R$ 99,62 (empregado) e R$ 33,21 (dependente).";
}
      } else if (msg.includes("obrigado") || msg.includes("obrigada") || msg.includes("valeu")) {
        resposta = "De nada! Se tiver mais alguma dúvida, é só perguntar.";
      } else if (msg.includes("tchau") || msg.includes("até logo") || msg.includes("fui")) {
        resposta = "Até logo! Se precisar de algo, estarei aqui para ajudar.";
      } else {
        resposta = "Desculpe, não entendi. Por favor, reformule sua pergunta.";
      }

      setTimeout(() => addMessage("ChatBot: " + resposta, "bot"), 500);
    }

    function addMessage(text, sender) {
      let chatBox = document.getElementById("chatBox");
      let messageElement = document.createElement("div");
      messageElement.className = "chat-message " + sender;
      messageElement.innerHTML = text;
      chatBox.appendChild(messageElement);
      chatBox.scrollTop = chatBox.scrollHeight;
    }

    document.getElementById("sendButton").addEventListener("click", sendMessage);
    document.getElementById("userInput").addEventListener("keypress", function(event) {
        if (event.key === "Enter") {
            sendMessage();
        }
    });

    // Mensagem de boas-vindas inicial do bot
    window.onload = function() {
      addMessage("ChatBot: Olá! Sou um assistente de informações da CAP. Posso responder sobre: <br>1. Elegibilidade <br>2. Prazos e Procedimentos <br>3. Plano UNIMED / HAPVIDA <br>4. Valores de Reembolso por Cargo", "bot");
    };
  </script>
</body>
</html>

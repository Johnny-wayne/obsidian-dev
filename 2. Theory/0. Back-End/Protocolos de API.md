
1) REST (Representational State Transfer, transferência de estado representacional)  
  
- Pense no REST como se você estivesse fazendo um pedido em um restaurante:  
- GET: Você pede para ver o cardápio  
- POST: Fazer um novo pedido  
- PUT/PATCH: Modificar seu pedido  
- DELETE: Cancelamento do pedido  
  
- REST é o protocolo mais amplamente usado para APIs da Web, operando em HTTP com métodos padrão como GET, POST, PUT e DELETE.  
  
2) GraphQL  
  
- O GraphQL é como preencher um formulário de pedido personalizado em um restaurante onde você pode escolher exatamente os ingredientes que deseja.  
  
- É uma alternativa mais flexível ao REST, permitindo que os clientes solicitem exatamente o que precisam em uma única solicitação.  
  
3) WebSockets  
  
- Os WebSockets fornecem comunicação bidirecional em tempo real entre cliente e servidor em uma única conexão de longa duração.  
  
- É como ter uma linha telefônica aberta em que ambas as partes podem falar a qualquer momento, o que o torna perfeito para:  
- Aplicativos de bate-papo  
- Notificações ao vivo  
- Atualizações em tempo real  
- Aplicativos de jogos  
  
4) MQTT (Transporte de Telemetria de Enfileiramento de Mensagens)  
  
- O MQTT usa um modelo de publicação/subscrição, no qual:  
- Os dispositivos podem publicar mensagens em tópicos específicos  
- Outros dispositivos podem se inscrever para receber essas mensagens  
- Um corretor gerencia a distribuição de mensagens  
  
- Ele foi projetado para dispositivos de IoT e situações em que a largura de banda da rede é limitada.  
  
5) Arquitetura sem servidor  
  
- A computação sem servidor permite que os desenvolvedores se concentrem no código sem gerenciar servidores.  
  
- Os principais aspectos incluem:  
- Dimensionamento automático com base na demanda  
- Você paga apenas pelo uso real  
- Não é necessário nenhum gerenciamento de servidor  
- Alta disponibilidade incorporada  
  
6) Quando usar cada tecnologia  
  
- REST é melhor para APIs gerais da Web devido à sua simplicidade e amplo suporte.  
  
- GraphQL é ideal para requisitos de dados complexos devido à sua flexibilidade de obtenção de dados.  
  
- WebSockets são perfeitos para aplicativos em tempo real que precisam de comunicação bidirecional.  
  
- O MQTT é ótimo para dispositivos IoT graças à sua natureza leve e eficiente.  
  
- O Serverless é melhor para aplicativos dimensionáveis sem gerenciamento de infraestrutura.  
  
Lembre-se de que essas tecnologias podem ser usadas juntas - elas não são mutuamente exclusivas. Por exemplo, você pode usar REST para sua API principal, WebSockets para recursos em tempo real e MQTT para comunicação com dispositivos IoT, tudo em uma arquitetura sem servidor.
![[1732198648355.gif]]
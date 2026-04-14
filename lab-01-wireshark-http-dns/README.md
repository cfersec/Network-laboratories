# Análise de Comunicação Web com Wireshark

## Objetivo
Analisar, na prática, o processo de comunicação entre cliente e servidor ao acessar um site, com foco nas etapas de resolução DNS, estabelecimento de conexão TCP e troca de dados via HTTP.

## Ferramentas Utilizadas
- Wireshark  
- Navegador web  
- Sistema operacional Linux (Kali)

## Procedimento
Iniciei a captura de pacotes no Wireshark utilizando a interface de rede ativa. Em seguida, acessei o domínio `example.com` por meio do navegador. Após o carregamento da página, interrompi a captura e apliquei filtros para visualizar especificamente os protocolos DNS, TCP e HTTP, facilitando a análise do fluxo de comunicação.

## Resultados Observados

### DNS
Foram identificados quatro pacotes relacionados à resolução de nomes:

<img width="1272" height="65" alt="image" src="https://github.com/user-attachments/assets/e9902996-8762-4271-96cd-91e9d9548ab9" />


- Duas requisições DNS:
  - Consulta do tipo A (IPv4)
  - Consulta do tipo AAAA (IPv6)

- Duas respostas:
  - Retorno com endereço IPv4
  - Retorno com endereço IPv6  

Essa sequencia indica que o sistema realizou consultas para os dois tipos de endereço IP.

---

### TCP
Após a resolução DNS, foi observado o estabelecimento da conexão TCP por meio do three-way handshake:

<img width="1128" height="65" alt="image" src="https://github.com/user-attachments/assets/3de2940f-8b0d-42ec-9489-c9937e105e40" />


- Envio de pacote SYN pela máquina cliente  
- Resposta do servidor com SYN/ACK  
- Confirmação com ACK enviado pelo cliente  

A conexão foi iniciada pela máquina local, utilizando uma porta efêmera (52258), com destino à porta 80 do servidor, associada ao serviço HTTP.

---

### HTTP
Com a conexão estabelecida, foi possível identificar a troca de dados no protocolo HTTP:

- Envio de uma requisição GET pelo cliente  
- Resposta do servidor contendo os dados da página  

Os dados foram transmitidos em segmentos TCP com flags PSH e ACK, indicando o envio de conteúdo da aplicação.

## Análise
Durante a análise, foi possível acompanhar o fluxo completo da comunicação:

1. O domínio é resolvido via DNS  
2. A conexão é estabelecida via TCP  
3. Os dados são transferidos via HTTP  

A observação desses eventos no Wireshark ajudou a conectar melhor os conceitos teóricos com o comportamento real da rede, principalmente na forma como os protocolos dependem uns dos outros.

## Conclusão
O laboratório permitiu validar, de forma prática, a relação entre os conceitos teóricos e o comportamento real da rede. Foi possível acompanhar sem dificuldades a sequência de eventos — resolução DNS, estabelecimento da conexão TCP e troca de dados via HTTP — e identificar cada etapa diretamente no Wireshark.

A visualização do tráfego contribuiu para reforçar o entendimento do fluxo completo de comunicação, confirmando na prática como os protocolos se organizam e interagem durante o processo.

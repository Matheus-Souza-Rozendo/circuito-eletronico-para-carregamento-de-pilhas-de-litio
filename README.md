# Circuito eletrônico para carregamento de pilhas de lítio

## Problema Inicial
Este projeto deriva de uma solução que foi criada para o cliente Dirceu B. Estes dados estão sendo mostrados com a autorização do mesmo

## Descrição do Projeto
Este projeto busca otimizar a eficiência e reduzir custos ao substituir o uso do Arduino Pro Mini por um circuito dedicado para controlar duas pilhas 18650/3,7V, um voltímetro 2S, um sensor óptico de linha e um micro servo 9g. A proposta inclui a criação de um circuito com saídas específicas para o voltímetro e o servo, além de uma entrada para o sensor, visando simplificação e economia. 

A integração de um BMS para proteção e carregamento das pilhas, juntamente com uma fonte CFTV 9V/2A, será consolidada em um único PCB bivolt, eliminando a necessidade de fontes externas. Em resumo, o projeto visa promover eficiência energética e redução de custos, destacando-se pela integração de componentes em uma solução coesa e adaptável no cenário de desenvolvimento tecnológico.

# Solução Apresentada
## ESTADOS DO SISTEMA
O sistema consiste de um servo motor (micro servo 9g) acionado por uma placa eletrônica. A entrada do sistema é um sensor óptico. Os estados do sistemas são os seguintes

**Estado 1:** Aguardando Acionamento do sensor - Acionado em 0°

**Estado 2:** esperando 1s na posição 0° - Acionado em 0°

**Estado 3:** rotacionando para 180° e aguardando 2s - Acionado em 180°

![Figura 5](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image5.png)

É possível notar pela figura 1 que o servo aguarda o sinal do sensor, depois aguarda 1 segundo sendo acionado na posição 0° e depois durante 3s(1s de deslocamento e 2 aguardando) é acionado na posição 180°..
Logo, vale salientar que não é possível realizar a leitura da posição no qual o servo está , usando uma placa sem microprocessador.

## CONTROLE DO SERVO MOTOR
Servomotores tem sua posição controlada variando a largura do pulso PWM, como mostrado na figura

![Figura 7](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image7.png)

Logo, a solução apresentada foi a criação de um circuito que gerasse sinal pwm com largura de 1ms e 2ms.Além disso, esse circuito deveria ser capaz de alterar entre seus dois estados por um controle digital feito por um circuito lógico combinacional.

O circuito resultante é mostrado na figura

![Figura 4](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image4.png)

Simulações feitas geraram os seguintes resultados

Sinal gerado colocando 6V na entrada 0° 

![Figura 1](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image1.png)

Sinal Gerado colocando 6V na entrada 180°

![Figura 8](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image8.png)

## Circuito Timer
Como discutido anteriormente, a transição do estado 1 para o estado 2 e do estado 2 para o estado 3 será feita utilizando-se do sinal proveniente de timers. Por isso, foi construído um circuito no qual um timer 555 no modo monoestável é acionado por um transistor e libera um sinal para a saída de 1 ou 3 segundos a depender da configuração de resistores utilizados.

![Figura 6](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image6.png)

Segue os resultados dos testes com esses circuitos

Timer de 1s - R1 de 900 KΩ

![Figura 3](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image3.png)

Timer de 3s - R1 de 2.7 MΩ

![Figura 3](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image3.png)

## CIRCUITO DIGITAL
Segue o link para baixar a simulação feita no  software circuitMaker

[Circuito Digital](https://github.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/blob/main/circuito%20logico.CKT)

## FONTE AC/DC PARA CARREGAR PILHAS

O circuito conversor AC/DC segue a linha de uma fonte linear regulada. Sua tensão de entrada é 12V AC. Por isso se faz necessário um transformador 220V para 12V.

A entrada da placa deve ser ligada nos terminais corretos do transformador.

O transformador recomendado é o [Mini Transformador De Energia Ei, Transformador De 220v, 6v, 9v, 12v, 15v, 24v, Entrada Dupla, 12v, 2w, Va - Transformadores - AliExpress.](https://m.pt.aliexpress.com/item/4000042064306.html?gatewayAdapt=Pc2Msite)

Qualquer outro transformador pode ser usado na instalação desde que seja com saída de 12V AC.

É utilizado também um módulo BMS 2S 3A para proteção das baterias de lítio.

Segue o esquema do circuito na figura

[Figura do Circuito](https://raw.githubusercontent.com/Matheus-Souza-Rozendo/circuito-eletronico-para-carregamento-de-pilhas-de-litio/main/images/image9.png)

## Recomendações

Não usar enquanto estiver conectado na tomada para evitar sobrecarga

Utilizar resistores e capacitores com o menor grau de erro possível

Conectar de forma adequada e conforme escrito na placa e no modelo enviado












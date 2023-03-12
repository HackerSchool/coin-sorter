# coin-sorter

*PT*

Este projecto consiste num sorteador de moedas por gravidade com deteção automática das moedas e contagem.
O microcontrolador usado é um Arduino UNO cujo programa corresponde ao único ficheiro de código presente no repositório.
Os restantes ficheiros são peças da caixa de suporte que tem a rampa de deslizamento e os slots das moedas.

## Electrónica
Para além do Arduino, é fundamentalmente necessário:
- 8 módulos do sensor de infravermelhos TCRT5000
- 1 módulo LCD1602 com adaptador I2C
- 1 botão e 1 resitência de 10k Ohms (montagem botão básica)

Na secção seguinte, descreve-se como estes componentes interagem com o I/O do Arduino.

## Programação
Como já mencionado, o ficheiro `coinsorter.ino` contém o código arduino que caracteriza todo o funcionamento. 

A library usada para comunicar com o módulo I2C do LCD é o Liquid Crystal:
```c++
LiquidCrystal_I2C lcd(0x3F, 16, 2);
// A4 - sda, A5 - clk
```
A configuração usa os [tradicionais](https://docs.arduino.cc/learn/communication/wire) pins A4 e A5 para o SDA/SCL do protocolo I2C.
O LCD precisa também das ligações habituais +5V e GND.

Cada módulo infravermelho do TCRT5000 corresponde a um tamanho de moeda diferente e estão ligados do pin 0 ao pin 7.
Definição:
```c++
const int IRinput[] = {0, 1, 2, 3, 4, 5, 6, 7};
```
Setup:
```c++
for(i = 0; i < 4; i++) pinMode(IRinput[i], INPUT);
```

O pushbutton é ligado ao pin A0.
Definição:
```c++
const int buttonPin = A0;
```
Setup:
```c++
pinMode(buttonPin, INPUT);
```

Uma versão melhorada deste setup e também da leitura inclui [Direct Port Manipulation](https://docs.arduino.cc/hacking/software/PortManipulation), e verá a luz do dia no futuro. Essencialmente é manipular directamente os registers I/O do arduino, excusando usar funções elaboradas que comem ciclos de relógio como quem bebe água.

## Modelação e Impressão
Os restantes ficheiros são para impressão 3d.
Uma descrição mais detalhada desta secção será adicionada no futuro, para que seja fácil de imprimir e assemblar as coisas.

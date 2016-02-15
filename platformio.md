# Compilador multi-plataforma platformio

O platformio permite manter um mesmo projeto para diferentes placas embarcadas.
As diferentes placas que este sistema suporta são listadas com o comando `platformio boards`. Este comando ainda aceita termos que limitem a busca por placas de um determinado fabricante ou que use determinado ambiente. Pode-se por exemplo usar `platformio boards arduino` para listar as placas que suportam a biblioteca arduino ou `platformio boards arm` para listar as placas que usam um microcontrolador arm.

Para usá-lo com a Launchpad com chip msp430g2553, por exemplo, crie um diretório vazio e execute o comando:
```bash
platformio init --board=lpmsp430g2553
```
Este comando fará com que sejam instalados o suporte necessário para a placa em questão, caso ainda não haja ou esteja desatualizado. Ele criará duas pastas e um arquivo:

- **src/** - Onde deve-se colocar o código fonte de seu projeto.
- **lib/** - Onde deve-se colocar bibliotecas próprias.
- **platformio.ini** - Que tem as configurações do projeto.

O arquivo **platformio.ini** contém as definições de cada ambiente de programação utilizado. Se quiser portar o código de uma placa para outra, basta acrescentar os dados da outra placa neste arquivo. Por enquanto não é necessário mexer nele.

Após acrescentar o código que se deseje no diretório **src** os comandos mais úteis são:
- `platformio run` para compilar o projeto.
- `platformio run --target upload` ou `platformio run -t upload` para enviar o projeto compilado (*firmware*) para a placa.
- `platformio run --target clean` para remover os arquivos compilados e manter apenas os códigos fonte.

## Exemplo: pisca-led para launchpad e arduino uno.

Primeiro cria-se o diretório onde ficará o projeto e inicializa-se o projeto:
```bash
mkdir piscaLed
cd piscaLed
platformio init --board=lpmsp430g2553 --board=uno
```

Estas duas placas suportam o que se chama do _framework_ arduino, portanto podemos escrever diretamente o código arduino e salvar em um arquivo .ino. Crie um arquivo piscaled.ino dentro do diretório src contendo um código arduino depara piscar o led no pino 13:
```c
void setup() {
  pinMode(13,OUTPUT);
}

void loop() {
  digitalWrite(13, LOW);
  delay(500);
  digitalWrite(13, HIGH);
  delay(500);
}
```

Basta então compilar o código (que vai ser compilado para as duas plataformas) e carregar na placa.
```bash
platformio run
platformio run target=upload
```

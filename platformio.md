# Compilador multi-plataforma platformio

O platformio permite manter um mesmo projeto para diferentes placas embarcadas.
As diferentes placas que este sistema suporta são listadas com o comando `platformio boards`

Para usá-lo com a FRDM-KL25Z, crie um diretório vazio e execute o comando:
```bash
platformio init --board=frdm_kl25z
```
Este comando fará com que sejam instalados o suporte necessário para a placa em questão e os compiladores. Ele criará duas pastas e um arquivo:

- **src/** - Onde deve-se colocar o código fonte de seu projeto.
- **lib/** - Onde deve-se colocar bibliotecas próprias.
- **platformio.ini** - Que tem as configurações do projeto.

O arquivo **platformio.ini** contém as definições de cada ambiente de programação utilizado. Se quiser portar o código de uma placa para outra, basta acrescentar os dados da outra placa neste arquivo. Por enquanto não é necessário mexer nele.

Após acrescentar o código que se deseje no diretório **src** os comandos mais úteis são:
- `platformio run` para compilar o projeto.
- `platformio run --target upload` ou `platformio run -t upload` para enviar o projeto compilado (*firmware*) para a placa.
- `platformio run --target clean` para remover os arquivos compilados e manter apenas os códigos fonte.

# Git para controle de versão local

O git é um sistema para controle de versões (Version Control System -VCS) voltado para desenvolvimento de software, muito embora possa ser usado em mais aplicações. Seu funcionamento é baseado num banco de dados (presente num diretório .git do projeto) que armazena as informações das diferentes versões de um projeto -- normalmente uma pasta específica.

Além disso o git tem um protocolo e ferramentas que permitem a sincronização do projeto local com uma versão externa (chamada repositório) que pode ser acessada por outras pessoas, habilitando que mais de uma pessoaa trabalhe no mesmo projeto.

O próprio material desta disciplina está armazenado num repositório aberto (público) no site github, que abriga vários projetos de código livre ou não. Pode-se criar uma cópia local deste projeto rodando o comando clone:
```
git clone https://github.com/joaopaulo-cerquinhocajueiro/sd2.git
```
Este comando vai criar uma pasta sd2 contendo todo o banco de dados das diferentes versões deste projeto no local em que foi executado. De dentro da pasta sd2 podemos ver uma lista destas diferentes versões usando o comando `git log`.

No git, cada versão definida no banco de dados é explicitamente criada pelo uso de um comando específico, o commit. O log é uma lista das vezes que foi rodado o commit, listando um identificador de cada commit (um código sha1, único para cada commit), o autor daquele commit, a data  e hora que ele ocorreu e um comentário a respeito do que foi modificado naquele commit em relação ao último. É comum se referenciar às versões como _commits_ ou então usar o verbo _commitar_.

![YUNO COMMIT](http://cdn.meme.am/instances/500x/65449283.jpg)

O git permite mudar o estado do projeto para qualquer uma das versões _commitadas_ através do comando checkout.

```
git checkout f8295fddab5d28db6658d25d1ed2440d6b46fa56
```
Isto funciona como uma _máquina do tempo_ do projeto. Todas modificações feitas no projeto após este commit são desfeitas, incluindo arquivos deletados ou excluídos (se estiverem no projeto; arquivos presentes na pasta do projeto nãonecessariamente são controlados pelo git).

Muitas vezes não é necessário ou útil mudar para aquela versão do projeto, mas sim comparar o que mudou de uma versão para outra. Para isto é útil o comando `diff`.

```
git diff f88ce395eb51df446c20fd2e41da93392145fd1d e01e9d89f962164fc5f7fa5751efa4efcbb315b2
```

O comando `diff` mostra a mudança linha a linha de diferentes versões do mesmo projeto. É muito útil para encontrar bugs novos, pois permite focar no que mudou no código de uma versão sem o bug para uma com.

## Criando um novo projeto.
A base de dados inicial de um novo projeto com o git é criada pelo comando `init`. Este comando pode ser executado numa pasta vazia ou já com algum material.

Crie uma pasta no seu computador e rode:
```
git init
git log
```

Para iniciar o controle de versão é necessário dizer ao git que arquivos ele irá controlar. Isto é feito pelo comando `add`. A criação de um commit é feita pelo comando `commit`, que obrigatoriamente irá pedir um comentário. Este comentário pode ser dado na própria linha de comando com a opção `-m"comentário"`.

```
edit 1.txt
git add 1.txt
git commit -m"Commit inicial"
git log
```
O git só salva a modificação que for dita a ele para salvar. Se for feita alteração em um arquivo (no 1.txt, por exemplo), esta alteração será ignorada num próximo commit a menos que mandemos que o git a considere. O comando status indica as modificações feitas.

```
git status
edit 1.txt
git status
git add 1.txt
git status
git commit -m"Alterado o 1.txt"
git status
edit 1.txt
edit 2.txt
git status
git add 2.txt
git status
git commit -m"Adicionado o 2.txt"
git status
git commit -a -m"Incrementado o 1.txt"
git status
```

Percebeu o que faz a opção -a no comando `commit`? Ela faz com que mudanças feitas num arquivo que já estava adiconado sejam acrescentadas ao commit.

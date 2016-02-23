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


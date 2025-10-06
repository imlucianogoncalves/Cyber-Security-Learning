# Linux Shells

> Aqui vou compartilhar minhas notas pessoais sobre cada um dos temas aprendidos no camihno Pentester do TryHackMe
## Bash

**[echo $SHELL]** mostra qual shell estámos usando naquele sistema.

**[cat /etc/shells]** mostra todos os shells que temos disponíveis naquela máquina.


## Fish

- Amigável, viável para usuários iniciantes.
- Correção ortográfica automática.
- Aplicar temas


---

Todo script em shell deve começar com o identificador do interpretador daquele shell.

Por exemplo, se quem for interpretar aquele código for o bash, usamos: **[#!/bin/bash]**

Antes de poder executar o shell, temos que dar a ele permissão de execução, isso é feito com **[chmod +x nome_do_arquivo.sh]**

Agora sim, para executar, usamos **[./nome-do-arquivo.sh]** neste caso, o "./" diz para executar tal shell.

Se deixarmos sem o "./", o bash vai tentar buscar aquele comando no caminho $PATH, e vai retornar erro pois le não está lá.

```
echo "Ola, qual e o seu nome?"

read nome

echo "Welcome, $nome"
```

Aqui, damos um echo e depois, pegamos o valor inputado pelo usuario e guardamos na variavel nome.

--- 

## Loop

```
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

Aqui, definimos a variável I e dizemos que ela irá iterar de 1 até 10.

A cada iteração, teremos um "do", que irá fazer os comandos abaixo dele. 

Quando estiver prontos, finalizamos com "done", que indica o fim.

```
#!/bin/bash

echo "Bem-vindo a ferramenta ultra secreta \n"
echo "Me diga seu nome primeiro"
read nome
if [ "$nome" = "Luciano" ]; then
        echo "Bem vindo, Luciano o segredo e: THM_Script"
else 
        echo "Foi mal, vc n pode entrar aqui n"
fi
```

Aqui, passamos um echo perguntando o nome e pegamos esse nome com o read para a variável nome.

Depois, a estrutura do if. onde `if [ "$nome" = "Luciano" ];` verificamos se o nome corresponde a "Luciano", se sim, com `then` enviamos uma ação (da linha debaixo).

Se não, passamos um `else` e sua respectiva ação.

Quando finalizamos a condição, aplicamos `fi`.

## Comentários

```
# Bem vindo bro
echo "Bem-vindo a ferramenta ultra secreta \n"

# Pergunta o nome 
echo "Me diga seu nome primeiro"

# Guarda o nome em uma varivel
read nome

# Checa se o nome corresponde
if [ "$nome" = "Luciano" ]; then

# Se sim, access granted
        echo "Bem vindo, Luciano o segredo e: THM_Script"
else
# Se nao, nao deixa
        echo "Foi mal, vc n pode entrar aqui n"
fi
```

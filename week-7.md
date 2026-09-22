---
layout: default
title: Semana 7 - Introdução ao Aprendizado de Máquina
---

# Semana 7 - Introdução ao Aprendizado de Máquina

Até aqui, estudamos problemas em que conseguíamos programar explicitamente um caminho para a solução. Nas buscas, definimos os estados, as ações possíveis e o objetivo. Na otimização, definimos as candidatas, as restrições, uma forma de comparar soluções e uma estratégia para melhorá-las. Em cada caso, fomos nós que escrevemos as regras que o computador deveria seguir.

Mas nem sempre conseguimos descrever boas regras de antemão. Como escrever todas as condições necessárias para reconhecer uma fruta, identificar uma mensagem indesejada ou prever se vai chover? Em aprendizado de máquina, usamos exemplos para construir um modelo capaz de fazer previsões sobre novos casos.

Nesta semana, vamos conhecer essa mudança de perspectiva. O objetivo não é decorar nomes de algoritmos, mas experimentar como exemplos podem nos ajudar a formular uma solução e como verificar se ela funciona em casos novos. Os nomes formais das etapas aparecerão depois da experiência.

## Roteiro de estudo

### 1. Entenda a mudança de perspectiva

Leia o texto **Aprendizado de Máquina**, de Ricardo Matsumura, até conseguir explicar com suas palavras:

- que diferença há entre programar diretamente todas as regras e construir uma solução a partir de exemplos;
- que tipo de resposta esperamos em um problema de classificação;
- por que acertar os exemplos conhecidos não basta.

Use o vídeo de introdução do H2IA para conhecer essas ideias por outro caminho. Enquanto acompanha, procure identificar os dados de entrada, a resposta esperada e o critério usado para dizer se uma previsão foi boa.

### 2. Pense em um primeiro problema

Imagine que temos uma tabela com a pressão e a umidade de vários dias e, para cada linha, sabemos se choveu ou não. Agora recebemos os valores de um novo dia e queremos fazer uma previsão.

Antes de procurar um algoritmo, tente responder:

1. Que informações do passado poderiam ajudar na decisão?
2. Como você transformaria os exemplos conhecidos em uma regra?
3. O que faria se casos parecidos tivessem respostas diferentes?
4. Como verificaria se sua regra funciona em dias que ela ainda não viu?

Uma possibilidade seria comparar o novo dia com os exemplos mais próximos. Outra seria procurar uma fronteira que separasse os casos de chuva e de não chuva. Essas ideias levam a diferentes algoritmos, que serão estudados ao longo do treinamento. Antes disso, a atividade desta semana permitirá experimentar o problema central: construir uma regra a partir de dados e verificar se ela funciona fora dos exemplos usados em sua criação.

### 3. Faça a atividade das frutas

Na atividade, você receberá uma tabela completa com exemplos de maçãs, tangerinas, laranjas e limões. Cada fruta tem massa, largura, altura e uma medida de cor. Sua tarefa é examinar os exemplos, formular sua própria estratégia e escrever uma função com `if`, `elif` e `else` que devolva o nome da fruta.

O notebook não indicará quais características ou intervalos usar. Não procure uma biblioteca que já faça a classificação. A parte importante é enfrentar a dificuldade de formular as regras, testá-las e perceber onde elas funcionam ou falham.

[Abra o notebook da atividade](https://drive.google.com/file/d/14cWezTGM5V8AzrbFg4VQx4dLzWibvwfw/view?usp=sharing)

> **Antes de editar:** abra o arquivo com o Google Colaboratory e use **Arquivo → Salvar uma cópia no Drive**. Trabalhe na sua própria cópia para não perder as alterações.

O notebook já contém o carregamento dos arquivos e os cálculos de avaliação. Você precisa completar a função de classificação, justificar suas escolhas e analisar os resultados.

### 4. Congele as regras antes de abrir o teste

Quando sua função estiver pronta:

1. registre a estimativa de quantas frutas novas ela acertará;
2. não altere mais as regras;
3. aplique a função ao conjunto de teste, que não mostra as respostas;
4. salve as previsões geradas pelo notebook;
5. espere a liberação do gabarito para avaliar o resultado.

Essa ordem é importante. Se você consultar as respostas do teste e continuar ajustando as regras, o conjunto deixa de representar exemplos realmente novos.

## Material de apoio

| Prioridade | Tipo | Material | Como usar |
| :--: | :--: | :-- | :-- |
| Principal | Texto | [Aprendizado de Máquina — Ricardo Matsumura](https://ricardomatsumura.medium.com/aprendizado-de-m%C3%A1quina-a3bbf2fa4051) | Leia para organizar as ideias de modelo, classificação e separação dos dados. |
| Principal | Vídeo | [Introdução ao Aprendizado de Máquina — H2IA](https://www.youtube.com/watch?v=RI3GVY4DL8s&t=6s) | Use como explicação geral e anote exemplos de entrada, saída e avaliação. |
| Complementar | Aula e notas | [CS50 AI — Learning](https://cs50.harvard.edu/ai/2020/weeks/4/) | Conheça vizinho mais próximo, KNN e separação por uma fronteira. Material em inglês. |
| Aprofundamento | Livro | Russell e Norvig, *Artificial Intelligence: A Modern Approach*, capítulo 19 | Referência opcional para aprofundar os conceitos depois da atividade. |

## Atividade: construindo regras para classificar frutas

### Parte 1 — observar e criar as regras

1. Abra o notebook no Colab e execute as células na ordem.
2. Examine com calma a tabela completa de exemplos conhecidos.
3. Decida por conta própria como procurar padrões e construir suas regras.
4. Escreva sua função de classificação usando apenas comparações e `if`, `elif` e `else`.
5. Aplique a função aos exemplos conhecidos, observe os erros e revise sua estratégia.
6. Encerre os ajustes quando chegar a uma solução que considere razoável e consiga explicar.

### Parte 2 — testar em frutas novas

Depois de congelar as regras, use o segundo arquivo do notebook. Ele tem as mesmas características, mas não mostra o nome das frutas. Gere e salve suas previsões.

O link do gabarito será liberado pelo professor depois dessa etapa. Ao recebê-lo, cole-o no local indicado no notebook e execute a avaliação. O notebook mostrará a acurácia total, a quantidade de acertos por classe, a matriz de confusão e os exemplos classificados incorretamente.

### O que entregar

- o notebook executado, com sua função e as respostas às perguntas;
- o arquivo `fruit_predictions.csv` gerado pelo notebook;
- uma breve comparação entre sua estimativa, o resultado nos exemplos conhecidos e o resultado no teste.

No fechamento da atividade, o notebook dará nome às etapas que você realizou. Não é necessário antecipar esses termos para começar: primeiro observe, crie as regras e teste.

[Voltar para o início](./)

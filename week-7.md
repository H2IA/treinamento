---
layout: default
title: Semana 7 - Introdução ao Aprendizado de Máquina
---

# Semana 7 - Introdução ao Aprendizado de Máquina

Nos encontros anteriores, vimos que um programa pode tomar uma decisão usando exemplos: um novo ponto próximo de exemplos de chuva provavelmente também representa chuva; vários vizinhos podem votar; ou uma reta pode separar duas regiões. Nesta semana, vamos organizar essas ideias e experimentar o processo completo em um problema pequeno.

O objetivo não é decorar nomes de algoritmos. Queremos entender que informações usamos para tomar uma decisão, como criamos uma regra a partir de exemplos e por que precisamos experimentar essa regra em dados que ainda não vimos.

## Roteiro de estudo

### 1. Comece pela pergunta

Leia o texto **Aprendizado de Máquina**, de Ricardo Matsumura, até conseguir explicar com suas palavras:

- que diferença há entre escrever todas as regras de um programa e ajustá-las a partir de exemplos;
- que tipo de resposta esperamos em um problema de classificação;
- por que acertar os exemplos conhecidos não basta.

Use o vídeo de introdução do H2IA para rever essas ideias por outro caminho. Enquanto acompanha, procure identificar os dados de entrada, a resposta esperada e o critério usado para dizer se uma previsão foi boa.

### 2. Retome os exemplos da aula

No exemplo da chuva, pressão e umidade eram características do dia, enquanto chuva ou não chuva era a resposta que queríamos prever. Primeiro usamos a proximidade entre pontos; depois consideramos vários vizinhos e uma separação por uma reta.

Antes de seguir, tente responder:

1. Como você classificaria um novo ponto muito próximo apenas de exemplos de chuva?
2. O que poderia acontecer se os vizinhos mais próximos discordassem?
3. Uma mesma reta consegue separar qualquer conjunto de pontos?
4. Como saber se uma regra continuará funcionando em exemplos novos?

### 3. Faça a atividade das frutas

Na atividade, você receberá exemplos de maçãs, tangerinas, laranjas e limões. Cada fruta tem massa, largura, altura e uma medida de cor. Sua tarefa é observar esses exemplos e escrever uma função com `if`, `elif` e `else` que devolva o nome da fruta.

Não procure uma biblioteca que já faça a classificação. A parte importante é formular as regras, testá-las e perceber onde elas funcionam ou falham.

[Abra o notebook da atividade no Google Colab](https://colab.research.google.com/github/H2IA/treinamento/blob/main/notebooks/atividade-frutas.ipynb)

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
| Revisão | Aula e notas | [CS50 AI — Learning](https://cs50.harvard.edu/ai/2020/weeks/4/) | Retome vizinho mais próximo, KNN e separação por uma fronteira. Material em inglês. |
| Aprofundamento | Livro | Russell e Norvig, *Artificial Intelligence: A Modern Approach*, capítulo 19 | Referência opcional para aprofundar os conceitos depois da atividade. |

## Atividade: construindo regras para classificar frutas

### Parte 1 — observar e criar as regras

1. Abra o notebook no Colab e execute as células na ordem.
2. Observe as primeiras linhas e a quantidade de exemplos de cada fruta.
3. Compare os valores mínimos e máximos das características por classe.
4. Escreva sua função de classificação usando apenas comparações e `if`, `elif` e `else`.
5. Aplique a função aos exemplos conhecidos e observe os erros.
6. Ajuste as regras somente com base nesses exemplos.
7. Explique quais características foram mais úteis e quais frutas foram mais difíceis de separar.

### Parte 2 — testar em frutas novas

Depois de congelar as regras, use o segundo arquivo do notebook. Ele tem as mesmas características, mas não mostra o nome das frutas. Gere e salve suas previsões.

O link do gabarito será liberado pelo professor depois dessa etapa. Ao recebê-lo, cole-o no local indicado no notebook e execute a avaliação. O notebook mostrará a acurácia total, a quantidade de acertos por classe, a matriz de confusão e os exemplos classificados incorretamente.

### O que entregar

- o notebook executado, com sua função e as respostas às perguntas;
- o arquivo `previsoes_frutas.csv` gerado pelo notebook;
- uma breve comparação entre sua estimativa, o resultado nos exemplos conhecidos e o resultado no teste.

No fechamento da atividade, o notebook dará nome às etapas que você realizou. Não é necessário antecipar esses termos para começar: primeiro observe, crie as regras e teste.

[Voltar para o início](./)

---
layout: default
title: Semana 8 - Classificação
---

# Semana 8 - Classificação

Na semana passada, você olhou uma tabela de frutas e escreveu à mão as condições que as separavam. Foi um trabalho de observar valores, propor um corte, testar, perceber o erro e tentar outro. Esta semana vamos entregar esse trabalho a um algoritmo.

A pergunta que organiza o assunto é simples: dado um exemplo, a que categoria ele pertence? Um e-mail é spam ou não; uma imagem mostra um gato, um cachorro ou um pássaro; um exame indica doença ou saúde. Em todos os casos, a resposta vem de um conjunto finito de classes, e o modelo aprende a escolher a partir de exemplos já rotulados.

Vamos estudar dois algoritmos que resolvem esse problema de maneiras opostas. A **árvore de decisão** aprende uma sequência de perguntas sobre os atributos, chegando a regras parecidas com as que você escreveu. O **k-NN** não aprende regra nenhuma: guarda os exemplos e decide por semelhança. Depois, uma parte igualmente importante: como medir se um classificador é bom. A acurácia sozinha engana, e veremos exatamente como.

## Roteiro de estudo

### 1. Situe o problema

Reveja nos slides a definição de classificação e as distinções iniciais: classificação e regressão, problemas binários, multiclasse e multirrótulo. Elas aparecem rápido, mas organizam o resto do assunto.

Guarde a ideia de **fronteira de decisão**: a região do espaço de atributos onde o modelo muda de resposta. Cada algoritmo desenha essa fronteira de um jeito, e é isso que os diferencia.

### 2. Entenda como a árvore escolhe suas perguntas

Esta é a parte central do roteiro, porque é o que você vai implementar. Acompanhe nos slides as três ideias, nesta ordem:

1. **o que é um corte**: uma pergunta de sim ou não sobre um atributo, que divide o grupo em dois;
2. **como medir a mistura de um grupo**: o índice de Gini, `G = 1 − Σ pᵢ²`, que vale zero quando o grupo tem uma classe só e cresce conforme ele se mistura;
3. **como comparar dois cortes**: a média ponderada do Gini dos dois lados, usando o tamanho de cada grupo como peso.

Refaça as contas do exemplo com lápis e papel antes de programar. Um grupo com 14 laranjas e 4 tangerinas tem `G = 1 − ((14/18)² + (4/18)²) ≈ 0,35`. O conjunto inteiro tem `G ≈ 0,71`. Se esses dois números saírem na sua mão, a implementação é só repetição.

O Gini não é o único critério. A entropia segue a mesma lógica — zero para um grupo puro, maior quanto mais misturado — e serve igualmente. Na atividade você pode usar qualquer um dos dois.

Se a escolha dos cortes não ficar clara nos slides, leia o texto **Aprendizado com Árvores de Decisão**, de Ricardo Matsumura, que percorre o mesmo caminho com outro exemplo.

### 3. Veja onde a árvore se perde

Sem nenhum limite, a árvore continua dividindo até cada folha ficar pura. Nos slides, isso produziu quatro perguntas novas só para separar três frutas, e uma regra como "altura ≤ 7,3 → laranja" que vale para um único exemplo do treino.

Ela acerta 48 de 48 no treino e não acerta mais nada no teste. Esse é o **overfitting**: o modelo decorou os exemplos em vez de capturar o padrão. A resposta é a **poda** — impor limites durante a construção, como profundidade máxima ou número mínimo de exemplos por folha, ou remover ramos depois.

Repare que o valor desses limites não pode ser escolhido olhando o treino, onde a árvore maior sempre vence. Ele é escolhido na validação.

### 4. Aprenda a medir

Metade da aula é sobre métricas, e não por acaso. Trabalhe o exemplo do teste de doença até conseguir reconstruí-lo:

- a **matriz de confusão** cruza a classe real com a prevista; a diagonal são os acertos;
- **TP, TN, FP e FN** são as quatro células de onde sai todo o resto;
- **acurácia** divide os acertos por todos os exemplos;
- **precisão** pergunta: dos que o modelo apontou como positivos, quantos eram;
- **revocação** pergunta: dos que eram positivos, quantos o modelo encontrou;
- **F1** resume as duas pela média harmônica.

Entenda por que o F1 usa a média harmônica e não a simples. O modelo "cauteloso" dos slides, que aponta um único doente e acerta, tem precisão 1,0 e revocação 0,1. A média simples lhe dá 0,55; o F1 dá 0,18. Um modelo que deixa nove de dez doentes sem diagnóstico não merece meio ponto.

### 5. Desconfie da acurácia

Um detector de fraude que responde sempre "legítima" acerta 99% das transações e não encontra fraude nenhuma. Quando uma classe é muito mais frequente que as outras, errar a minoritária custa pouco na média, e o modelo aprende a ignorá-la.

Conheça as quatro saídas da aula — métricas por classe, reamostragem, pesos de classe e ajuste do limiar de decisão — e guarde a regra prática: reamostre apenas o treino, e avalie sempre na distribuição real.

O texto **Lidando com Desbalanceamento de Classes**, de Ricardo Matsumura, detalha essas estratégias. Leia antes de escolher qual vai experimentar na atividade.

Na atividade você vai encontrar esse problema de frente, e não como exemplo ilustrativo: o conjunto de frutas foi ampliado com duas classes raras.

### 6. Deixe o k-NN para o fim

O k-NN aparece na aula antes da árvore, mas na atividade ele é opcional e vem depois, como comparação. A ideia é curta: para classificar um exemplo novo, encontre os `k` mais parecidos no treino e escolha a classe mais votada entre eles. Não há fase de treino; o modelo é o próprio conjunto de dados.

Dois detalhes valem a atenção. O primeiro é a **escala**: a distância soma as diferenças de todos os atributos, então um atributo que varia em centenas domina um que varia em unidades. Nos slides, usar os quatro atributos sem normalizar derrubou o resultado de 39 para 27 acertos; normalizados, subiu para 47. O segundo é o **k**: pequeno demais é sensível a ruído, grande demais suaviza; o valor se escolhe na validação.

### 7. Observe a diferença entre explicar e acertar

Os dois modelos explicam suas decisões, de formas diferentes. O k-NN explica por exemplos: "é limão porque quatro das cinco frutas mais parecidas eram limões". A árvore explica por regras: "é maçã porque a cor é maior que 0,82".

Nos slides, essa segunda explicação está perfeitamente clara e completamente errada — a fruta era uma laranja. **Explicável não é o mesmo que correto.** Guarde isso para a última pergunta da atividade.

## Material de apoio

| Prioridade | Tipo | Material | Como usar |
| :--: | :--: | :-- | :-- |
| Principal | Slides | [Slides da aula: Classificação](https://drive.google.com/file/d/1m3zrJduPANOTi6a4KNc4MncSDO4CZvcY/view?usp=sharing) | Fonte principal do roteiro. Acesse com sua conta institucional `@inf`. Refaça as contas de Gini e as métricas do exemplo de doença. |
| Principal | Texto | [Aprendizado com Árvores de Decisão — Ricardo Matsumura](https://ricardomatsumura.medium.com/aprendizado-com-%C3%A1rvores-de-decis%C3%A3o-73d874664d1) | Leia junto com o passo 2 para ver a escolha dos cortes explicada por outro caminho. |
| Principal | Texto | [Lidando com Desbalanceamento de Classes — Ricardo Matsumura](https://ricardomatsumura.medium.com/lidando-com-desbalanceamento-de-classes-38a56bfafd3) | Leia antes da parte 5 da atividade, para escolher a estratégia que vai experimentar. |
| Complementar | Vídeo | [Decision and Classification Trees, Clearly Explained! — StatQuest](https://www.youtube.com/watch?v=_L39rN6gz7Y) | Percorre a construção de uma árvore com o Gini, incluindo atributos contínuos e overfitting. Veja se o passo 2 do roteiro não fechar. Em inglês, com legendas. |
| Complementar | Vídeo | [Machine Learning Fundamentals: The Confusion Matrix — StatQuest](https://youtu.be/Kdsp6soqA7o) | Monta a matriz de confusão do zero, no caso binário e no multiclasse. Use antes da parte 3 da atividade. Em inglês, com legendas. |

## Atividade: implementando uma árvore de decisão

Você vai implementar uma árvore de decisão do zero e usá-la para classificar as frutas. Não use bibliotecas que já forneçam o algoritmo: `pandas` e `numpy` são bem-vindos para organizar os dados, mas a escolha dos cortes, a construção da árvore e as métricas são suas.

[Abra o notebook da atividade](https://drive.google.com/file/d/1_BGEMCOujDhOW75OnzOW713F7fU5HA1R/view?usp=sharing)

> **Antes de editar:** acesse o arquivo com sua conta institucional `@inf`, abra-o com o Google Colaboratory e use **Arquivo → Salvar uma cópia no Drive**. Trabalhe na sua própria cópia para não perder as alterações.

### Os dados mudaram

O conjunto da semana passada foi ampliado. Além de maçã, tangerina, laranja e limão, agora existem **toranjas** e **limas**: 56 frutas no treino e 15 no teste. As duas classes novas têm poucos exemplos, e a tangerina continua pequena. Esse desequilíbrio é a matéria-prima da parte de métricas.

Suas regras escritas à mão na semana passada não conhecem as classes novas, então os resultados não são diretamente comparáveis. Guarde-as mesmo assim: no fim, a comparação que interessa é entre as perguntas, não entre os acertos.

### Parte 1 — a impureza e o corte

1. Implemente uma função que receba um grupo de rótulos e devolva sua impureza. Use o Gini da aula ou a entropia, e registre qual escolheu.
2. Confira a função com os números da aula antes de seguir: um grupo puro deve dar zero, e o grupo de 14 laranjas e 4 tangerinas deve dar aproximadamente 0,35.
3. Decida quais limiares testar. Para um atributo contínuo há infinitos, mas quase todos são equivalentes: só mudam de verdade os cortes que caem entre dois valores presentes no grupo. Ordene os valores distintos e use o ponto médio entre consecutivos — ou os próprios valores, se preferir. Registre a escolha.
4. Implemente a comparação entre dois cortes. Cada lado é um grupo, e você já sabe medir sua impureza; falta ponderar os dois pelo tamanho. A média simples não serve: um corte que isola uma única fruta deixa aquele lado puro sem que isso signifique nada.
5. Junte as duas coisas na busca: percorra todos os atributos e todos os limiares, descarte os cortes que deixam um lado vazio e devolva o de menor custo.
6. Aplique a busca ao conjunto completo. O primeiro corte da árvore da aula foi `color_score <= 0,825`.

Confira as funções auxiliares em um caso pequeno antes de rodá-las no conjunto inteiro. É muito mais fácil achar um erro em quatro valores que você consegue verificar de cabeça.

### Parte 2 — construir e ler a árvore

7. Implemente a construção recursiva, com `max_depth` e `min_samples_leaf` como parâmetros.
8. Construa uma árvore com profundidade máxima 3 e imprima-a.
9. Leia-a de cima para baixo como uma sequência de perguntas e compare com as regras que você escreveu à mão: quais atributos o algoritmo usou? Ignorou algum que você considerava essencial?

### Parte 3 — as métricas

10. Implemente a matriz de confusão para as seis classes.
11. Implemente precisão, revocação e F1 por classe. Trate o denominador zero: ele vai acontecer.
12. Aplique as métricas à árvore de profundidade 3 e responda: **quais classes o modelo nunca prevê?** A acurácia total deixava isso visível? Por que o algoritmo as abandonou?

A resposta dessa última pergunta está na média ponderada: um grupo pequeno pesa pouco no custo de um corte, então criar um ramo para três frutas quase nunca compensa.

### Parte 4 — profundidade, poda e validação

13. Compare árvores de profundidades diferentes, incluindo sem limite nenhum. Para cada uma, registre a acurácia no treino, o número de folhas e a revocação das classes raras.
14. A árvore sem limite acerta tudo no treino. Explique por que esse número não serve para compará-la com as outras.
15. Implemente a validação *leave-one-out*: para cada fruta, construa a árvore com as outras 55 e preveja a que ficou de fora. Use essa estimativa — e não o treino — para escolher a profundidade.
16. Olhe a tabela da validação e responda: **a poda ajudou neste conjunto?**

Essa última pergunta é aberta de verdade, e a resposta pode muito bem ser não. São 56 frutas; uma diferença de duas ou três previsões entre duas árvores não distingue nada. Se os números não sustentarem a poda, diga isso — e então justifique sua escolha final por outro critério, como o tamanho da árvore ou a facilidade de explicá-la. Concluir que a poda ajudou porque *deveria* ajudar é o erro que esta etapa existe para evitar.

### Parte 5 — um experimento com o desbalanceamento

17. Experimente uma das estratégias da aula e veja o efeito nas métricas por classe. A mais direta é o *oversampling*: replicar os exemplos das classes raras no treino. Diga se a revocação delas melhorou e se alguma outra métrica piorou junto.

Vale para qualquer estratégia que você escolha: altere apenas o conjunto de treino. Avaliar em dados reamostrados mede o modelo em uma distribuição que não existe.

### Parte 6 — congelar e testar

18. Escolha uma única árvore final e registre a escolha, junto com uma estimativa de quantas das 15 frutas novas ela acertará.
19. Não altere mais o modelo. Gere as previsões para o teste e salve o arquivo `tree_predictions.csv`.
20. Depois da liberação do gabarito, execute a avaliação e analise a matriz de confusão e as métricas por classe.
21. Ainda com o gabarito em mãos, aplique **também** a árvore sem limite ao teste e compare com a sua escolhida. Agora você tem os dois números: o da validação e o do teste. Eles contam a mesma história?

Vale a mesma regra da semana passada: se você consultar as respostas do teste e continuar ajustando o modelo, o conjunto deixa de representar exemplos realmente novos.

### Parte 7 — comparar com o k-NN (recomendada)

Esta parte é opcional no sentido de que a entrega é aceita sem ela. Mas é aqui que está o resultado mais interessante da atividade, e quem parar antes vai perder a melhor pergunta da semana: **por que dois algoritmos corretos, treinados nos mesmos dados, discordam tanto?**

Implemente o k-NN e compare-o com a árvore usando a mesma validação. Nessa comparação:

- avalie com e sem normalização min-max, e explique a diferença pela escala dos atributos;
- teste valores diferentes de `k` e observe o efeito nas classes raras — com `k = 5`, uma classe de três exemplos consegue vencer alguma votação?
- compare o tipo de explicação que cada modelo oferece para uma mesma previsão;
- se um dos dois vencer com folga, explique **por quê**, olhando a forma dos dados. A árvore só consegue cortar paralelo aos eixos, uma pergunta por atributo de cada vez; o k-NN enxerga vizinhanças em qualquer direção. Que formato os agrupamentos de frutas têm no espaço de atributos, e qual dos dois esse formato favorece?

### O que analisar

No fechamento do notebook, responda:

1. As perguntas escolhidas pelo algoritmo foram parecidas com as regras que você escreveu à mão? Ele usou os mesmos atributos? Chegou a algum corte que não teria lhe ocorrido?
2. O resultado no teste ficou acima ou abaixo da sua estimativa? E em relação ao treino?
3. Quais confusões aparecem fora da diagonal da matriz? São entre frutas parecidas?
4. As classes raras foram previstas no teste? Sua estratégia de desbalanceamento ajudou?
5. A poda ajudou? Responda com os números da validação e os do teste, e diga se os dois concordam.
6. Escolha uma previsão errada e explique, percorrendo a árvore, por que o modelo chegou a ela. Se sua árvore acertou todo o teste, use um erro da validação — eles não faltam. Uma decisão explicável é por isso mesmo uma decisão correta?
7. Se o problema fosse triagem médica em vez de frutas, qual erro você preferiria cometer: um falso positivo ou um falso negativo? Que métrica acompanharia?

### Como entregar

Entregue o notebook executado, com as saídas visíveis, e o arquivo `tree_predictions.csv` gerado por ele.

[Voltar para o início](./)

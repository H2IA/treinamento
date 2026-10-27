---
layout: default
title: Semana 9 - Regressão Linear
---

# Semana 9 - Regressão Linear

Nas duas últimas semanas, a resposta do modelo era o nome de uma fruta. Uma previsão estava certa ou errada, e contar os acertos era o ponto de partida para avaliar. Esta semana a resposta passa a ser um número: em vez de *a que classe este exemplo pertence?*, vamos perguntar **quanto?**

Quando a resposta é um número em uma escala contínua, o problema é de **regressão**. Prever o preço de um imóvel, a temperatura de amanhã ou o tempo de entrega de um pedido são exemplos. Uma previsão de 150 para um valor real de 160 não está "errada" do mesmo jeito que uma previsão de 300: as duas erram, mas por distâncias muito diferentes. Medir essa distância é o que organiza todo o assunto.

Vamos estudar o modelo mais simples e mais usado para esse problema, a **regressão linear**. Ela procura a reta, ou o plano, que passa mais perto dos exemplos conhecidos. Você vai encontrá-la de duas maneiras: por uma fórmula fechada, que dá a resposta de uma vez, e pelo **gradiente descendente**, que chega à mesma resposta dando pequenos passos — uma ideia que retoma a busca local da semana 6 e reaparece em quase todo o aprendizado de máquina que vem depois.

Os dados também mudam. Deixamos as frutas e passamos a um conjunto clássico de regressão: 442 pacientes com diabetes, com dez medidas tomadas no início do acompanhamento — idade, sexo, IMC, pressão arterial e seis exames de sangue — e uma medida de quanto a doença progrediu um ano depois.

## Roteiro de estudo

### 1. Situe o problema

Reveja a distinção da semana passada: em classificação, a resposta vem de um conjunto finito de classes; em regressão, de uma escala numérica. Os dados continuam sendo uma tabela com características `X` e uma resposta `y`, e a separação entre treino e teste continua valendo. O que muda é o tipo de `y` e, por consequência, como medimos o erro.

Antes de abrir qualquer material, pense: se você soubesse apenas o IMC de um paciente, como estimaria a progressão da doença? E se não soubesse nada sobre ele, qual seria o palpite mais razoável?

### 2. Entenda o modelo

Com um único atributo, o modelo é uma reta:

`ŷ = w · x + b`

O peso `w` é a inclinação: quanto a progressão prevista aumenta para cada ponto a mais de IMC. O viés `b` é o valor previsto quando `x` vale zero — muitas vezes sem significado nenhum, já que ninguém tem IMC zero, mas necessário para a reta passar no lugar certo.

Para cada exemplo, a diferença `y − ŷ` entre o valor real e o previsto é o **resíduo**. Uma boa reta deixa resíduos pequenos. Para transformar todos eles em um único número, a regressão linear usa o **erro quadrático médio**:

`MSE = (1/n) · Σ (yᵢ − ŷᵢ)²`

Elevar ao quadrado faz duas coisas: impede que erros para cima e para baixo se cancelem, e pune mais os erros grandes. Um erro de 40 conta quatro vezes mais que um de 20, não duas. Guarde essa consequência: ela explica por que um único exemplo muito fora do padrão pode puxar a reta inteira.

Leia o módulo **Regressão linear** do curso de Machine Learning do Google até a parte de perda. O vídeo **The Main Ideas of Fitting a Line to Data**, do StatQuest, mostra a mesma ideia de forma visual.

### 3. Encontre a melhor reta com uma fórmula

Para um único atributo, a reta que minimiza o MSE tem solução fechada, chamada de **mínimos quadrados**:

`w = Σ (xᵢ − x̄)(yᵢ − ȳ) / Σ (xᵢ − x̄)²`
`b = ȳ − w · x̄`

Em palavras: a inclinação mede o quanto `x` e `y` variam juntos, dividido pelo quanto `x` varia sozinho; e a reta sempre passa pelo ponto médio `(x̄, ȳ)`.

Refaça as contas com lápis e papel antes de programar. Três pacientes com IMC 22, 26 e 30 e progressão 110, 160 e 180 têm `x̄ = 26` e `ȳ = 150`, o que dá `w = 280 / 32 = 8,75` e `b = 150 − 8,75 · 26 = −77,5`. As previsões são 115, 150 e 185, os resíduos são −5, 10 e −5, e o MSE é 50. Se esses números saírem na sua mão, a implementação é só repetição.

### 4. Encontre a mesma reta descendo pelo erro

A fórmula fechada não se generaliza bem para modelos mais complexos. A alternativa é tratar o ajuste como um problema de otimização, exatamente como na semana 6: começamos com pesos quaisquer e os melhoramos aos poucos.

A diferença é que agora não precisamos testar vizinhos um a um. O MSE é uma função suave dos pesos, e sua derivada — o **gradiente** — aponta a direção em que o erro mais cresce. Basta dar um passo na direção oposta:

`w ← w − α · ∂MSE/∂w`
`b ← b − α · ∂MSE/∂b`

O número `α` é a **taxa de aprendizado**. Pequena demais, o algoritmo leva uma eternidade; grande demais, ele salta por cima do mínimo e o erro explode. Na atividade você vai provocar os dois casos de propósito.

Lembre do problema do ótimo local no hill climbing. Na regressão linear, o MSE tem a forma de uma tigela: há um único mínimo, e descer sempre leva até ele. Essa garantia é rara e vale a pena perceber que ela existe aqui — nos modelos que virão depois, ela desaparece.

Assista ao vídeo **Gradient Descent, Step-by-Step**, do StatQuest, que ajusta exatamente uma reta com esse método e deriva as contas passo a passo. Depois volte ao módulo do Google, na parte de gradiente descendente e hiperparâmetros.

### 5. Use mais de um atributo

Com vários atributos, o modelo vira `ŷ = w₁x₁ + w₂x₂ + … + b`. O gradiente descendente funciona sem mudança nenhuma: cada peso recebe a sua própria derivada. A fórmula fechada também existe, na forma das **equações normais**, `(XᵀX) w = Xᵀy`: um sistema linear com uma equação por peso.

Três cuidados aparecem aqui:

- **Escala.** Você já a encontrou no k-NN. O colesterol total varia em centenas; o `s5`, entre 3 e 6. Uma mesma taxa de aprendizado é grande demais para um e pequena demais para o outro. Padronizar os atributos — subtrair a média e dividir pelo desvio padrão do treino — resolve isso.
- **Interpretação dos pesos.** Com atributos correlacionados, o peso de um deles depende de quais outros estão no modelo. Neste conjunto, o colesterol total (`s1`) e o LDL (`s2`) têm correlação de 0,90: dizem quase a mesma coisa. Um peso não é a "importância" de um atributo isolado, e às vezes nem o sinal dele quer dizer o que parece.
- **A tigela achatada.** Quando dois atributos dizem quase a mesma coisa, há muitas combinações de pesos que erram quase igual. A tigela continua tendo um único fundo, mas vira um vale comprido e plano, e o gradiente descendente anda devagar ao longo dele.

### 6. Aprenda a medir

Três métricas aparecem em quase todo problema de regressão:

- o **MAE**, erro absoluto médio, diz quanto o modelo erra em média, na unidade da resposta;
- o **RMSE**, raiz do MSE, também está na unidade da resposta, mas pesa mais os erros grandes;
- o **R²** compara o modelo com o palpite mais simples possível, que é prever sempre a média do treino: `R² = 1 − Σ(y − ŷ)² / Σ(y − ȳ)²`.

O R² vale 1 quando o modelo acerta tudo e 0 quando ele não é melhor que a média. Pode até ser negativo. Repare no paralelo com a semana passada: lá, um modelo que respondia sempre a classe mais frequente servia de comparação para a acurácia; aqui, a média cumpre esse papel.

Não espere um R² perto de 1 neste conjunto. Dez medidas tomadas em um dia não determinam como uma doença vai evoluir em um ano; uma parte da variação simplesmente não está nos dados. Um modelo honesto aqui explica cerca de metade dela, e saber reconhecer esse limite também é parte do trabalho.

### 7. Linear nos pesos, não nos atributos

A regressão linear só sabe somar atributos multiplicados por pesos. Mas nada impede que um atributo seja construído a partir de outros: um quadrado, um produto, uma razão. O modelo continua linear nos pesos e continua sendo ajustado do mesmo jeito.

Isso abre uma porta perigosa. Com dez atributos, todos os quadrados e produtos entre pares somam mais de sessenta colunas, e com elas o modelo sempre erra menos no treino. Você já viu esse filme na semana passada, com a árvore sem limite: errar menos no treino não é o mesmo que prever melhor. A escolha de atributos se faz na validação.

## Material de apoio

| Prioridade | Tipo | Material | Como usar |
| :--: | :--: | :-- | :-- |
| Principal | Texto | [Regressão linear — Curso de Machine Learning do Google](https://developers.google.com/machine-learning/crash-course/linear-regression?hl=pt-br) | Fonte principal do roteiro. Leia as partes de modelo e perda antes do passo 3, e as de gradiente descendente e hiperparâmetros antes do passo 4. |
| Principal | Vídeo | [Gradient Descent, Step-by-Step — StatQuest](https://www.youtube.com/watch?v=sDv4f4s2SB8) | Ajusta uma reta com gradiente descendente, derivando cada passo. Assista antes da parte 3 da atividade. Em inglês, com legendas. |
| Complementar | Vídeo | [The Main Ideas of Fitting a Line to Data — StatQuest](https://www.youtube.com/watch?v=PaFPbb66DxQ) | Mostra visualmente o que significa minimizar a soma dos quadrados dos resíduos. Use se o passo 2 não fechar. Em inglês, com legendas. |
| Complementar | Vídeo | [Linear Regression, Clearly Explained!!! — StatQuest](https://www.youtube.com/watch?v=nk2CQITm_eo) | Apresenta o R² e a regressão com vários atributos. Use antes da parte 2 da atividade. Em inglês, com legendas. |
| Complementar | Livro | Christopher M. Bishop, *Neural Networks for Pattern Recognition*, seção 1.2 | Leitura sugerida para consolidar o roteiro depois dos passos 1 e 2. Em inglês. |
| Complementar | Dados | [Diabetes dataset — scikit-learn](https://scikit-learn.org/stable/datasets/toy_dataset.html#diabetes-dataset) | Descrição oficial do conjunto usado na atividade. Leia antes de começar, para saber o que cada coluna mede. |
| Aprofundamento | Livro | Russell e Norvig, *Artificial Intelligence: A Modern Approach*, capítulo 19, seção sobre regressão linear | Referência opcional para a forma matricial e a derivação completa do gradiente. |

## Atividade: prevendo a progressão do diabetes

Você vai implementar a regressão linear do zero e usá-la para prever a progressão do diabetes a partir das medidas iniciais de cada paciente. Não use bibliotecas que já forneçam o algoritmo: `pandas` e `numpy` são bem-vindos para organizar os dados e fazer as contas — inclusive `numpy.linalg.solve` para resolver o sistema das equações normais —, e `matplotlib` para os gráficos. O ajuste, o gradiente, a validação e as métricas são seus.

[Abra o notebook da atividade](https://colab.research.google.com/github/H2IA/treinamento/blob/main/notebooks/atividade-regressao.ipynb)

> **Antes de editar:** abra o notebook no Google Colaboratory e use **Arquivo → Salvar uma cópia no Drive**. Trabalhe na sua própria cópia para não perder as alterações.

### Os dados

O conjunto **Diabetes** é distribuído com o scikit-learn. Usamos a versão com os valores originais, sem padronização, dividida uma única vez em 354 pacientes de treino e 88 de teste. O arquivo de teste não traz a progressão; o gabarito será liberado pelo professor depois que você congelar o modelo.

A resposta, `progression`, varia de 25 a 346 no treino, com média em torno de 153. Guarde essa escala: um RMSE de 50 é pequeno ou grande conforme a comparação com ela.

Os dados são reais, mas o objetivo é estudar o modelo, não tirar conclusões clínicas. A documentação nem informa qual código de `sex` corresponde a cada sexo.

### Parte 1 — uma reta, pela fórmula

1. Implemente o ajuste por mínimos quadrados para um único atributo, devolvendo `w` e `b`.
2. Confira a função com o exemplo do roteiro antes de seguir: os IMCs 22, 26 e 30 e as progressões 110, 160 e 180 devem dar `w = 8,75` e `b = −77,5`.
3. Ajuste a progressão em função do IMC, usando os 354 pacientes. Interprete o peso: quanto a progressão prevista aumenta por ponto de IMC? O viés tem algum significado?
4. Desenhe os pontos e a reta no mesmo gráfico. Os pontos ficam perto da reta?

### Parte 2 — as métricas

5. Implemente o MAE, o RMSE e o R².
6. Calcule as três para o palpite que prevê sempre a média do treino. Confirme que o R² dá zero e diga por quê.
7. Calcule as três para retas usando apenas o IMC, apenas o `s5` e apenas a pressão (`bp`). Qual medida isolada explica melhor a progressão? Quanto da variação ela deixa sem explicar?

### Parte 3 — a mesma reta, pelo gradiente

8. Derive no papel as duas derivadas do MSE, em relação a `w` e a `b`. Confira com o vídeo do StatQuest.
9. Implemente o gradiente descendente para vários atributos, guardando o MSE a cada passo. Comece com todos os pesos em zero.
10. Rode-o com o IMC como único atributo, sem padronizar, e compare os pesos com os da fórmula. Anote quantos passos foram necessários: com os valores brutos, são mais de cem mil.
11. Rode-o com os dez atributos **sem padronizar** e depois **padronizando**. Para cada caso, teste algumas taxas de aprendizado e desenhe a curva do MSE ao longo dos passos. Encontre uma taxa que diverge e uma que converge devagar demais.

Padronize usando a média e o desvio padrão do treino, e guarde esses valores. Os pacientes de teste precisam ser transformados com os mesmos números; calculá-los de novo no teste faria o modelo receber atributos numa escala diferente daquela em que foi ajustado.

### Parte 4 — vários atributos, pela fórmula

12. Implemente o ajuste pelas equações normais: acrescente uma coluna de uns à matriz de atributos padronizados, para o viés, e resolva `(XᵀX) w = Xᵀy` com `numpy.linalg.solve`.
13. Ajuste os dez atributos pelos dois métodos e compare o MSE no treino e os pesos, um a um. Os erros quase coincidem? E os pesos de `s1` e `s2`?
14. Aumente o número de passos do gradiente descendente e veja os pesos de `s1` e `s2` se aproximarem dos da fórmula. O que acontece com o MSE enquanto isso?
15. Compare o peso de `s1` em um modelo só com ele e no modelo com os dez atributos. O sinal mudou? Explique usando a correlação entre `s1` e `s2`.

Leve a sério a pergunta sobre o sinal. Um peso negativo para o colesterol total não quer dizer que mais colesterol protege o paciente. Quer dizer que, **mantidos fixos os outros atributos — em especial o LDL —**, os pacientes com mais colesterol total têm, em média, progressão menor — e, como os dois andam quase sempre juntos, essa situação quase não aparece nos dados.

### Parte 5 — escolher os atributos

16. Implemente a validação cruzada com `k = 5` partes: sorteie a ordem dos pacientes uma vez, divida-os em cinco grupos e, para cada grupo, ajuste o modelo com os outros quatro e preveja o que ficou de fora. É a generalização do *leave-one-out* da semana passada, que aqui exigiria 354 ajustes por modelo.
17. Compare, pela validação, pelo menos estes modelos: só IMC; IMC e `s5`; IMC, `bp` e `s5`; os dez atributos.
18. Construa ao menos um atributo novo — um quadrado ou um produto entre dois atributos — e veja se ele melhora a validação. Diga por que esperava que melhorasse.
19. Para cada modelo, compare também o erro no treino com o da validação. A distância entre eles cresce conforme o modelo ganha atributos?

Com 354 pacientes, a validação é bem mais estável que nas semanas anteriores, mas não é exata: um ou dois pontos de diferença no RMSE não distinguem nada. Se dois modelos empatarem, escolha pelo outro critério que a situação pede — o mais simples, o que você consegue explicar — e diga isso.

### Parte 6 — olhar os resíduos

20. Para o modelo que você escolheria, calcule os resíduos da validação e desenhe-os contra a progressão prevista. O tamanho dos erros é parecido em toda a faixa, ou muda?
21. Desenhe os resíduos contra o IMC. Há alguma curva, ou eles parecem espalhados ao acaso?
22. Agrupe os resíduos pelo valor de `sex` e calcule a média de cada grupo. Faz sentido usar um código 1 ou 2 como se fosse uma medida? O que mudaria se houvesse três categorias?

Um modelo bom deixa resíduos que parecem ruído: sem padrão, sem tendência, sem um grupo puxando para um lado. Quando os resíduos têm estrutura, eles estão contando algo que o modelo deixou de fora.

### Parte 7 — congelar e testar

23. Escolha um único modelo final e registre a escolha, junto com uma estimativa do RMSE que ele terá nos 88 pacientes de teste.
24. Não altere mais o modelo. Ajuste-o com os 354 pacientes, gere as previsões para o teste e salve o arquivo `progression_predictions.csv`.
25. Depois da liberação do gabarito, execute a avaliação e compare o RMSE com a sua estimativa e com o da validação.
26. Ainda com o gabarito em mãos, avalie também os outros modelos candidatos no teste. A ordem entre eles é a mesma da validação?

Vale a mesma regra das semanas anteriores: se você consultar as respostas do teste e continuar ajustando o modelo, o conjunto deixa de representar pacientes realmente novos.

### Parte 8 — muitos atributos (recomendada)

Esta parte é opcional no sentido de que a entrega é aceita sem ela. Mas é aqui que aparece, em regressão, o mesmo fenômeno da árvore sem limite.

27. Construa todos os quadrados e produtos entre pares dos dez atributos, além dos próprios atributos. Descarte `sex²`: com só dois valores, ele repete a coluna `sex`.
28. Ajuste esse modelo pelas equações normais e compare o R² no treino e na validação com os do modelo de dez atributos.
29. Ajuste o mesmo modelo pelo gradiente descendente, com uma taxa pequena e poucos passos, e compare a validação de novo. A taxa que funcionava com dez atributos agora diverge: descubra por quê.
30. O gradiente descendente interrompido cedo validou melhor que a solução exata? Explique, pensando no que os pesos ainda não tiveram tempo de fazer.

### O que analisar

No fechamento do notebook, responda:

1. A fórmula e o gradiente descendente chegaram aos mesmos pesos? O que a padronização mudou no gradiente descendente — e o que ela não mudou nas previsões finais?
2. O que o peso do IMC no modelo de um atributo significa? Ele continua igual quando os outros atributos entram? Por quê?
3. O que aconteceu com o peso de `s1` quando `s2` entrou no modelo? Você usaria os pesos desse modelo para dizer qual exame "importa mais"?
4. O R² do seu melhor modelo ficou longe de 1. Isso indica um erro na implementação, um modelo ruim ou um limite dos dados? Como você distinguiria esses casos?
5. Que padrão você encontrou nos resíduos? O que ele sugere que o modelo não captura?
6. O resultado no teste ficou acima ou abaixo da sua estimativa? A ordem dos modelos se manteve?
7. Um paciente novo tem IMC 48, acima de qualquer paciente do treino. Você confiaria na previsão do seu modelo para ele? O que pode dar errado quando um modelo é usado fora da faixa dos exemplos em que foi ajustado?
8. Se este modelo fosse usado para decidir quais pacientes recebem acompanhamento mais próximo, que tipo de erro seria mais grave: superestimar ou subestimar a progressão? Alguma das métricas que você implementou distingue os dois?

### Como entregar

Entregue o notebook executado, com as saídas visíveis, e o arquivo `progression_predictions.csv` gerado por ele.

[Voltar para o início](./)

---
layout: default
title: Semana 6 - Otimização e Metaheurísticas
---

# Semana 6 - Otimização e Metaheurísticas

Até aqui, procuramos uma sequência de movimentos que leva um tabuleiro até a configuração desejada. Agora vamos estudar problemas em que queremos escolher uma boa configuração, como os itens de uma mochila com capacidade limitada.

Para decidir o que levar, precisamos definir quais seleções são permitidas e como comparar duas delas. Podemos atribuir um valor a cada seleção e procurar aumentá-lo. Em outro problema, podemos querer reduzir um erro ou um custo. Esse é o ponto de partida da otimização.

## Antes de começar

Para acompanhar a ideia, você precisa entender funções, comparações e repetições. Não é necessário ter implementado A*. A atividade usa também vetores: aqui, pense em um vetor como uma lista de números que descreve uma candidata à solução.

## Roteiro de estudo

### 1. Definir o que estamos procurando

Escolha um exemplo pequeno de mochila: quatro itens, cada um com um peso e um valor, e uma capacidade que impeça levar tudo. Liste as seleções que cabem e compare seus valores.

Nesse exemplo, uma candidata é uma seleção de itens. A capacidade define uma restrição, e a soma dos valores é a **função objetivo** que queremos maximizar. O algoritmo é a estratégia escolhida para procurar uma boa candidata. Podemos trocar de algoritmo sem mudar o problema.

### 2. Tentar melhorar uma solução

Assista à [aula de Optimization do CS50](https://youtu.be/qK46ET1xk2A?si=aq0byCExowo6MTRB), começando pela parte de busca local e hill climbing. Os exemplos são diferentes da mochila, mas a pergunta é a mesma: que pequena mudança podemos fazer na solução atual?

Chamamos de **vizinhança** o conjunto de candidatas que podemos obter com as mudanças permitidas. Na mochila, uma escolha possível é adicionar, remover ou trocar um item, sempre respeitando a capacidade. No hill climbing, comparamos vizinhos e avançamos para uma melhora.

O método pode parar porque nenhum vizinho melhora o resultado, mesmo existindo uma seleção melhor em outra região. Esse é um ótimo local, definido em relação à vizinhança. Um ótimo global é o melhor resultado entre todas as candidatas permitidas. Para minimização, a melhora é uma redução no valor; para maximização, é um aumento.

### 3. Procurar alternativas quando a melhora acaba

Continue na aula com reinícios e simulated annealing. Um reinício começa uma nova busca de outro ponto. O simulated annealing pode aceitar uma piora, com uma probabilidade que depende de seu tamanho e de um parâmetro chamado temperatura. Assim, a busca pode sair de uma região onde só melhorar a cada passo não seria suficiente.

Separe duas informações durante a execução: a candidata atual e a melhor já encontrada. Ao aceitar uma piora, elas podem deixar de coincidir. Experimente prever o que acontece com a chance de aceitar a mesma piora quando a temperatura diminui.

Essa discussão costuma aparecer como **exploração e aproveitamento**: visitar outras regiões ou insistir em melhorar as que já parecem boas. Reinícios e aceitação de pioras ajudam a explorar, mas uma execução curta não garante encontrar o ótimo global.

### 4. Ampliar o repertório

Use os slides para revisar os métodos e consultar busca tabu e algoritmos genéticos. A busca tabu restringe temporariamente certas mudanças para evitar retornos imediatos. Algoritmos genéticos mantêm uma população de candidatas e produzem novas combinações por seleção, cruzamento e mutação.

Você não precisa implementar todos os métodos para começar. Entenda uma execução de hill climbing e uma de simulated annealing antes de escolher os dois algoritmos da atividade.

O vínculo com aprendizado de máquina aparece quando a candidata passa a ser um conjunto de parâmetros de um modelo e a função objetivo mede seu erro nos dados. Esse será um dos assuntos seguintes; por enquanto, concentre-se em como definir e comparar candidatas.

### Material de Apoio

| Tipo | Tópico | Descrição | Link |
| :--: | :----- | :-------- | :--: |
| Vídeo | **Optimization, CS50** | Aula principal do roteiro. Acompanhe as explicações de busca local, hill climbing, reinícios e simulated annealing. | [Assistir](https://youtu.be/qK46ET1xk2A?si=aq0byCExowo6MTRB) |
| Slides | **Slides da aula: Otimização** | Slides para acompanhar o estudo de otimização. | [Acessar](https://drive.google.com/file/d/1wvmSlzfdCDfTaY9C6CWxFopAToS9x4AP/view?usp=sharing) |
| Slides | **Slides complementares** | **Busca em Espaços (Thiago Reis Porto):** otimização, mínimos local/global, exploration vs. exploitation e metaheurísticas. | [Acessar](https://docs.google.com/presentation/d/1ioLN5dje44bmHv2cdeF7xFvfW_WKW2IFrJ7lxEj38pw/edit?usp=sharing) |

As [notas de Optimization do CS50](https://cs50.harvard.edu/ai/notes/3/) ficam como consulta complementar para rever as definições e o pseudocódigo depois de assistir à aula. A aula e as notas estão em inglês e incluem assuntos além do recorte desta semana.

### Atividade principal: escolhendo os itens da mochila

Você vai usar busca local para decidir quais itens colocar em uma mochila. Cada item tem um peso e um valor, mas a mochila suporta no máximo **275 unidades de peso**. O objetivo é encontrar uma seleção de itens com o maior valor total possível sem ultrapassar essa capacidade.

Esta atividade foi dividida em etapas. Primeiro você vai entender o problema e representar uma solução. Depois vai implementar um hill climbing, observar uma limitação do método e testar reinícios aleatórios.

#### Dados do problema

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| :-- | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: | --: |
| Peso | 63 | 21 | 2 | 32 | 13 | 80 | 19 | 37 | 56 | 41 | 14 | 8 | 32 | 42 | 7 |
| Valor | 13 | 2 | 20 | 10 | 7 | 14 | 7 | 2 | 2 | 4 | 16 | 17 | 17 | 3 | 21 |

#### Etapa 1: comece com um caso pequeno

Considere apenas os itens 1, 2, 3 e 4 e uma mochila com capacidade 70. Antes de programar, responda:

1. Quais seleções de itens respeitam a capacidade?
2. Qual delas tem o maior valor total?
3. Calcule a razão `valor/peso` de cada item. Depois, tente adicionar os itens da maior para a menor razão, sempre que couberem. A seleção obtida é a melhor que você encontrou na pergunta anterior?
4. O que esse resultado mostra sobre usar uma regra simples para tomar cada decisão separadamente?

O objetivo desta etapa não é procurar rapidamente a resposta. É identificar as três partes do problema: as candidatas possíveis, a restrição de peso e o valor usado para compará-las.

#### Etapa 2: represente e avalie uma solução

Represente uma candidata por uma lista com 15 posições. Use `1` quando o item estiver na mochila e `0` quando ele ficar de fora. Por exemplo, a candidata abaixo leva apenas os itens 1 e 3:

```python
[1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

Implemente funções que recebam uma candidata e calculem:

- seu peso total;
- seu valor total;
- se ela é viável, isto é, se o peso não ultrapassa 275.

Teste essas funções com a mochila vazia, com uma candidata viável e com uma candidata que ultrapasse a capacidade. Mostre os resultados no notebook.

#### Etapa 3: defina a vizinhança

Duas candidatas serão vizinhas quando diferirem em uma única posição. Assim, um movimento adiciona ou remove exatamente um item. Descarte uma vizinha quando ela ultrapassar a capacidade.

Implemente uma função que gere todas as vizinhas viáveis de uma candidata. Antes de continuar, escolha uma candidata simples e confira manualmente se a função gerou as vizinhas esperadas.

#### Etapa 4: implemente o hill climbing

Implemente o algoritmo seguindo estas regras:

1. comece com uma candidata viável;
2. gere todas as suas vizinhas viáveis;
3. escolha a vizinha com maior valor total;
4. avance somente se essa vizinha melhorar estritamente o valor da candidata atual;
5. pare quando nenhuma vizinha produzir melhora.

Em caso de empate entre vizinhas, escolha primeiro a de menor peso. Se o empate continuar, mantenha a primeira encontrada. Essa regra torna o comportamento reproduzível.

Durante a execução, registre pelo menos a candidata atual, seu peso, seu valor e o número de avaliações da função objetivo. Conte uma avaliação sempre que o algoritmo calcular o valor de uma candidata para decidir se deve escolhê-la.

Use primeiro como ponto inicial a candidata que contém os itens **6, 7, 8, 9, 10 e 14**. Observe o que acontece e responda:

- O algoritmo fez algum movimento?
- A solução encontrada parece boa?
- Por que ela pode ser um ótimo local quando usamos essa vizinhança?
- Permitir a troca simultânea de um item por outro mudaria as vizinhas disponíveis?

#### Etapa 5: acrescente reinícios aleatórios

Uma única execução depende do ponto inicial. Agora execute o hill climbing a partir de **20 candidatas iniciais viáveis** e guarde a melhor solução encontrada.

Para gerar cada candidata inicial de forma reproduzível:

1. comece com a mochila vazia;
2. embaralhe a ordem dos itens usando um gerador pseudoaleatório com semente registrada;
3. percorra os itens nessa ordem e, para cada um, faça um sorteio com 50% de chance de tentar adicioná-lo;
4. adicione o item somente quando o sorteio permitir e ele ainda couber.

Apresente uma tabela com o peso e o valor final de cada reinício. Destaque o melhor resultado e informe o total de avaliações da função objetivo realizado nas 20 execuções.

#### O que analisar

No final do notebook, responda com suas palavras:

1. Por que o hill climbing pode parar mesmo quando ainda existe uma solução melhor?
2. Os reinícios encontraram sempre o mesmo resultado? O que isso mostra sobre o ponto inicial?
3. Qual foi o melhor valor encontrado? Quais itens formam essa solução e qual é seu peso?
4. O maior número de reinícios garante que encontraremos a melhor solução possível? Explique.
5. Que mudança você faria na vizinhança ou na estratégia para tentar escapar de um ótimo local?

#### Regras de implementação

- Implemente o hill climbing e os reinícios sem usar bibliotecas prontas de otimização.
- Bibliotecas como `random`, `numpy`, `pandas` e `matplotlib` podem ser usadas para sorteios, organização dos resultados e gráficos, mas não para fornecer o algoritmo de busca.
- Organize o notebook de modo que outra pessoa consiga executar as células na ordem e reproduzir os resultados.
- Explique as escolhas importantes. O código funcionando é parte da entrega, mas a análise do comportamento do algoritmo também é obrigatória.

### Desafio extra opcional: Função de Rastrigin

Se quiser aprofundar a atividade, implemente **dois algoritmos de busca** e use-os para minimizar a Função de Rastrigin. Este desafio não substitui a atividade principal da mochila e pode ser entregue como uma seção adicional do mesmo notebook ou em outro notebook.

```text
f(x) = 10·n + Σ [xᵢ² - 10·cos(2π·xᵢ)], para i = 1..n
```

O mínimo global é `f(x) = 0` em `x = (0, 0, ..., 0)`. Use o intervalo `[-5.12, 5.12]` para cada coordenada. Trabalhe primeiro em duas dimensões para conferir o cálculo e observar as propostas de movimento. Depois faça a comparação em **10 ou mais dimensões**.

No desafio:

- implemente dois métodos entre hill climbing, random-restart, simulated annealing, busca tabu ou algoritmo genético;
- defina e registre a vizinhança ou forma de gerar candidatas e o tratamento de propostas fora dos limites;
- use o mesmo limite de avaliações da função objetivo para comparar os métodos;
- quando houver sorteios, faça várias execuções com sementes registradas e mostre a variação dos resultados;
- apresente a melhor solução, o valor de `f(x)`, o número de avaliações e o critério de parada de cada método;
- discuta como o ponto inicial e os parâmetros influenciaram os resultados e como cada método equilibrou exploração e aproveitamento.

Não chame o fim de uma execução de “convergência” apenas porque o limite de avaliações foi atingido. Informe se ela terminou pelo orçamento, pela ausência de melhora ou por outro critério.

### Como Entregar

Suba sua solução da atividade da mochila (o notebook `.ipynb` do Colab e quaisquer arquivos) no seu repositório **`treinamento-h2ia`** no GitHub. Se tiver feito o desafio da Rastrigin, inclua-o no mesmo repositório. Depois envie o **link do repositório** através do formulário abaixo:

| Tipo | Descrição | Link |
| :--: | :-------- | :--: |
| Formulário | **Formulário de Entrega:** envie aqui o link do seu repositório no GitHub | [Enviar Trabalho](https://docs.google.com/forms/d/e/1FAIpQLSeaoaM-Pi3uI0ZrLtPtn3O8tnfko79evU4OOQPdMIi4q0LuDQ/viewform) |

> Certifique-se de que o repositório esteja **público** (ou compartilhado) e que o notebook esteja salvo com as saídas das execuções visíveis.

[Voltar para o início](./)

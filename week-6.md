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

### Atividade: Otimizando a Função de Rastrigin

Sua missão é implementar **dois algoritmos de busca do zero** e usá-los para **minimizar** uma função conhecida por ser um "campo minado" de mínimos locais: a **Função de Rastrigin**.

**Regras do desafio:**

- Implemente **dois** algoritmos entre os vistos na aula (ex.: Hill Climbing, Random-Restart, Simulated Annealing, Tabu Search ou Algoritmo Genético).
- Escreva os algoritmos **do zero**: **sem** bibliotecas de otimização prontas (`scipy.optimize`, frameworks de GA, etc.) e **sem** auxílio de IA. O objetivo é entender o funcionamento na prática.
- Use `numpy` apenas para a matemática vetorial, se quiser.

**O problema: Função de Rastrigin:**

```
f(x) = 10·n + Σ [ xᵢ² − 10·cos(2π·xᵢ) ]   , para i = 1..n
```

- **Mínimo global:** `f(x) = 0` em `x = (0, 0, ..., 0)`.
- Trabalhe com **10 ou mais dimensões** (`n ≥ 10`). O termo do cosseno cria inúmeros mínimos locais, o que torna a otimização desafiadora e ótima para comparar estratégias.

**Ao final, apresente:**

- A melhor solução encontrada por cada algoritmo e o valor da função objetivo `f(x)`;
- O número de avaliações da função objetivo e o critério usado para encerrar a execução;
- Uma **comparação** entre os dois métodos: quem chegou mais perto do mínimo global? Quem foi mais rápido? Como cada um lidou com o dilema *exploration vs. exploitation*?
- Reflita: o quanto o **ponto inicial** e os **parâmetros** (passo, temperatura, taxa de mutação, etc.) afetaram o resultado?

## Como começar e comparar os resultados

Antes de executar em 10 dimensões, use duas dimensões para conferir o cálculo da função e observar algumas propostas de movimento. Esse é um passo de preparação; a comparação pedida na atividade continua sendo com 10 ou mais dimensões.

Defina o intervalo permitido para cada coordenada e o que seu algoritmo faz quando uma proposta sai dele. O enunciado não fixa esse intervalo, então registre a escolha e use a mesma nos dois métodos. Declare também a regra de vizinhança ou de geração de novas candidatas.

Use o mesmo limite de avaliações da função objetivo para comparar os métodos. Uma iteração de um algoritmo pode avaliar um vizinho, enquanto a de outro avalia uma população inteira. Por isso, contar apenas iterações pode esconder uma diferença grande no trabalho realizado.

Se houver sorteios, repita a comparação com várias sementes e registre os resultados de cada execução. Mostre a variação, além do melhor resultado. Nos métodos que partem de um único ponto, use os mesmos pontos iniciais nas comparações. Documente a inicialização dos demais métodos.

Não chame o encerramento de “convergência” apenas porque o limite de avaliações foi atingido. Diga se a execução parou pelo orçamento, pela ausência de melhora ou por outro critério que você definiu.

Antes de entregar, tente explicar por que um resultado pode ser ótimo entre os vizinhos e ainda estar longe do melhor possível. Mostre também onde seu código guarda a melhor candidata, mesmo quando a atual piora.

### Como Entregar

Suba sua solução (o notebook `.ipynb` do Colab e quaisquer arquivos) no seu repositório **`treinamento-h2ia`** no GitHub e envie o **link do repositório** através do formulário abaixo:

| Tipo | Descrição | Link |
| :--: | :-------- | :--: |
| Formulário | **Formulário de Entrega:** envie aqui o link do seu repositório no GitHub | [Enviar Trabalho](https://docs.google.com/forms/d/e/1FAIpQLSeaoaM-Pi3uI0ZrLtPtn3O8tnfko79evU4OOQPdMIi4q0LuDQ/viewform) |

> Certifique-se de que o repositório esteja **público** (ou compartilhado) e que o notebook esteja salvo com as saídas das execuções visíveis.

[Voltar para o início](./)

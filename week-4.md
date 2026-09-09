---
layout: default
title: Semana 4 - Buscas Sem Informação
---

# Semana 4 - Buscas Sem Informação

![Alt image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*VM84VPcCQe0gSy44l9S5yA.jpeg)
_Imagem retirada de [Breaking Down Breadh-First Search](https://medium.com/basecs/breaking-down-breadth-first-search-cebe696709d9)_

Imagine um quebra-cabeça com oito peças e um espaço vazio. Você pode deslizar uma peça vizinha para o espaço vazio, mas como escolher uma sequência de movimentos que coloque tudo em ordem?

Esse será nosso primeiro problema de busca. Antes de escolher um algoritmo, precisamos descrever o tabuleiro, os movimentos permitidos e a configuração que queremos alcançar. Depois, precisamos decidir em que ordem experimentar as possibilidades.

## Antes de começar

Você vai usar listas, funções, condições e repetições em Python. Se ainda não está confortável com esses recursos, retome a [semana 2](week-2.md). Para começar a entender o problema, porém, basta desenhar um tabuleiro e fazer alguns movimentos no papel.

## Roteiro de estudo

### 1. Representar o problema

Comece pela parte de buscas sem informação da aula “Search”, do CS50. Observe como um problema vira estados e ações. No quebra-cabeça, o estado é a disposição de todas as peças, incluindo o espaço vazio. Uma ação é um movimento permitido; a transição é o novo tabuleiro produzido por esse movimento.

Desenhe um tabuleiro e todos os tabuleiros que podem surgir depois de uma jogada. Faça mais uma jogada em um deles. Você consegue voltar ao estado anterior? Essa repetição será importante quando passarmos ao código.

### 2. Escolher o que explorar primeiro

Continue com BFS e DFS. A fronteira guarda as possibilidades descobertas que ainda aguardam análise. A BFS usa uma fila para explorar primeiro as mais antigas; a DFS usa uma pilha para explorar primeiro as mais recentes. Mantendo o restante da implementação igual, essa mudança altera a ordem da busca.

Um nó de busca guarda um estado e informações sobre o caminho até ele, como o nó anterior e o movimento realizado. Isso permite reconstruir a solução. Dois nós podem conter o mesmo tabuleiro e ter chegado a ele por caminhos diferentes.

Antes de executar o exemplo do vídeo, pause e tente prever qual nó sairá da fronteira. Depois veja se a sua previsão estava certa.

### 3. Passar da ideia à implementação

A aula de Dave Churchill aprofunda a organização da busca e a comparação entre os métodos. Use-a depois de conseguir acompanhar um exemplo pequeno de fila e pilha. Preste atenção ao tratamento de estados repetidos e à diferença entre o caminho da solução e todos os nós que o algoritmo precisou explorar.

No nosso quebra-cabeça, cada movimento custa 1. Nessas condições, a BFS encontra uma solução com o menor número de movimentos, quando existe solução. A DFS pode encontrar um caminho mais longo. O custo de guardar a fronteira também merece atenção: uma solução curta não significa necessariamente uma busca pequena.

### 4. Consultar outra explicação

O texto de Ricardo Matsumura ajuda a revisar o vocabulário em português. O capítulo de Russell e Norvig fica como aprofundamento, especialmente para as propriedades e a complexidade dos algoritmos. O Red Blob Games oferece exemplos interativos para comparar estratégias.

Alguns desses recursos também tratam de heurísticas e A*. Você pode deixar essas partes para a semana 5. Primeiro, procure explicar uma execução de BFS e de DFS sem depender do vídeo.

### Material de Apoio

Siga a ordem do roteiro; os materiais de consulta podem ser retomados conforme aparecerem dúvidas.

| Tipo | Tópico                    | Descrição                                                                                               |                                                       Link                                                        |
| :--: | :------------------------ | :------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------: |
| Slides | **Slides da aula: Buscas** | Slides para acompanhar o estudo de buscas. | [Acessar](https://drive.google.com/file/d/1apKudeSNBhu1rGrKrG4B7cd-S2fhmwvN/view?usp=sharing) |
| Vídeo | **Conceito Visual**       | **CS50 - Search (Harvard):** Representação de problemas, fronteira, BFS e DFS.                          |                              [Assistir](https://www.youtube.com/watch?v=WbzNRTTrX0g)                              |
| Vídeo | **Lógica Prática**        | **Dave Churchill - Intro to AI:** Fila, pilha e diferenças entre busca em árvore e em grafo. |                              [Assistir](https://www.youtube.com/watch?v=m9lPatLXE8s)                              |
| Texto | **Teoria**                | **Algoritmos de Busca (Ricardo Matsumura):** Explicação didática e em português.                        | [Acessar](https://ricardomatsumura.medium.com/algoritmos-de-busca-para-intelig%C3%AAncia-artificial-7cb81172396c) |
| Livro | **Referência**            | **Capítulo 3 - Russell & Norvig:** Para quem quer o rigor matemático (Opcional/Consulta).               |           [Acessar](https://drive.google.com/file/d/1c_dFxt3KONbV7Z-r5Cr0smG8siCAe3le/view?usp=sharing)           |
| Interativo | **Exemplo interativo** | **Red Blob Games:** Explicação dos algoritmos e exemplos interativos para ver como eles se comportam    |                   [Acessar](https://www.redblobgames.com/pathfinding/a-star/introduction.html)                    |

### Atividade: O Quebra-Cabeça (8-Puzzle)

Sua tarefa prática será implementar um agente capaz de resolver o clássico **Quebra-Cabeça de Blocos Deslizantes** (8-Puzzle).

O computador receberá o tabuleiro embaralhado e deverá nos dizer a sequência exata de movimentos para ordená-lo.

1. Crie seu repositório `treinamento-h2ia` (se ainda não criou).
2. Prepare seu ambiente Jupyter/Colab. Use [Modelo de Relatório.](https://colab.research.google.com/drive/1dQf8LOmDxFZFxQIOCO2MJDh_shXa-tnj?usp=sharing)
3. Tente implementar a estrutura de "Nó" e "Estado" conforme estudado.
4. Implemente (em ordem de dificuldade, vá até onde conseguir):

   - Busca em profundidade
   - Busca em largura
   - Busca em profundidade com aprofundamento iterativo

5. Compare os algoritmos usando os mesmos tabuleiros iniciais. Registre o tamanho da solução, a quantidade de nós expandidos, o maior tamanho da fronteira e o tempo. O tamanho da fronteira é um indicador parcial do armazenamento, não uma medida de toda a memória usada.

Comece por um tabuleiro a um ou dois movimentos do objetivo, produzido a partir dele por movimentos válidos. Confira se cada passo devolvido pelo algoritmo é permitido e se o caminho termina no objetivo. Depois aumente a dificuldade.

O aprofundamento iterativo repete uma busca em profundidade com limites crescentes. Estude primeiro a versão com limite de profundidade. Ao repetir a busca com um limite maior, reinicie suas estruturas; guardar os visitados da rodada anterior pode impedir a exploração necessária.

## Antes de seguir

Você consegue explicar por que o programa não deve continuar indo e voltando entre dois tabuleiros? E por que encontrar uma solução com DFS não prova que ela seja a mais curta? Use uma execução pequena do seu código para sustentar as respostas.

[Voltar para o início](./)

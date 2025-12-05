---
layout: default
title: Semana 4 - Buscas Sem Informação
---

# Semana 4 - Buscas Sem Informação

![Alt image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*VM84VPcCQe0gSy44l9S5yA.jpeg)
_Imagem retirada de [Breaking Down Breadh-First Search](https://medium.com/basecs/breaking-down-breadth-first-search-cebe696709d9)_

Nesta semana, iremos começar as implementações e de fato dar o ponta-pé inicial. Começaremos introduzindo conceitos da inteligência artificial clássica.

**Você já parou pra pensar:**

- Como o **Google Maps** ou **Waze** encontram o caminho mais curto entre a sua casa e a faculdade com incontáveis caminhos a serem percorridos?
- Como uma IA de xadrez decide a próxima jogada analisando milhões de possibilidades?
- Como um robô aspirador sabe como sair de um quarto sem bater nas paredes?

Nesta semana iremos aprender um assunto que parece um pouco distante do que esperamos do hype da IA, mas de extrema importância e que resolve e auxilia em diversos problemas como os supracitados.

### 📅 Roteiro de Estudos

Para que o nosso encontro prático seja produtivo, montamos um **caminho guiado**. Siga a ordem a seguir para construir seu conhecimento passo a passo. Sinta-se a vontade para pesquisar outros materiais e compartilhá-los no nosso canal de discussão.

Importante dizer que os materiais citados a seguir vão além do conteúdo dessa semana. Fiquem a vontade para já irem aprofundando, mas saibam que ainda entraremos nos assuntos de busca com heurísticas e otimização, portanto é opcional por hora.

#### 1. A Visão Geral (Visualizando o Problema)

Antes de pensar em código, precisamos entender **o que** o computador está tentando fazer. Portanto escolhemos a aula **"Search - CS50"** (Link na tabela abaixo) para introduzir o assunto de representação e buscas.

Esse recurso introduz de forma bastante didática buscas com exemplos visuais. Aqui é explorado também os algoritmos de **Busca em Largura (BFS)** e **Profundidade (DFS)** e a implementação desses algoritmos.

A ideia é que vocês comecem a entender onde esse assunto se insere, como representar estados e ações e como esses algoritmos resolvem o problema.

#### 2. Aprofundando

Agora que você já está mais familiarizado com a ideia, o próximo vídeo que julgamos interessante é o **"Problem Solving and Search - Dave Churchill"**. Aqui igualmente ao recurso anterior, é uma aula introdutória, mas que se traz um conteúdo mais denso e teórico.

Este vídeo é bastante importante para a sua implementação. Ele mostra que a única diferença entre uma **BFS** e **DFS** é a estrutura de dados e vai além. Como esses algoritmos se comportam em termos de performance e espaço? Qual é a complexidade de um para o outro?

Importante prestar atenção pois você terá de fazer essa análise das suas implementações.

#### 3. Consolidando o Conhecimento com o Ricardo do Medium

Para fechar a teoria e garantir que os termos estão claros. Leia o artigo do **Ricardo Matsumura**. Aqui a ideia é consolidar o conhecimento e fazer o paralelo dos termos em inglês para o português, com uma revisão didática do professor Ricardo do Medium.

### 4. Extras

Elencamos também o livro do Russel e Norvig com o capítulo de buscas opcionalmente com o rigor matemático e teórico.

### 📚 Material de Apoio

Reunimos os materiais que julgamos mais interessantes

| Tipo | Tópico                    | Descrição                                                                                               |                                                       Link                                                        |
| :--: | :------------------------ | :------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------: |
|  🎥  | **Conceito Visual**       | **CS50 - Search (Harvard):** A melhor visualização de labirintos e Fronteiras.                          |                              [Assistir](https://www.youtube.com/watch?v=WbzNRTTrX0g)                              |
|  🎥  | **Lógica Prática**        | **Dave Churchill - Intro to AI:** A diferença crucial entre Fila vs. Pilha e Busca em Árvore vs. Grafo. |                              [Assistir](https://www.youtube.com/watch?v=m9lPatLXE8s)                              |
|  📄  | **Teoria**                | **Algoritmos de Busca (Ricardo Matsumura):** Explicação didática e em português.                        | [Acessar](https://ricardomatsumura.medium.com/algoritmos-de-busca-para-intelig%C3%AAncia-artificial-7cb81172396c) |
|  📘  | **Referência**            | **Capítulo 3 - Russell & Norvig:** Para quem quer o rigor matemático (Opcional/Consulta).               |           [Acessar](https://drive.google.com/file/d/1c_dFxt3KONbV7Z-r5Cr0smG8siCAe3le/view?usp=sharing)           |
|  🎮  | **Algoritmos Interativo** | **Red Blob Games:** Explicação dos algoritmos e exemplos interativos para ver como eles se comportam    |                   [Acessar](https://www.redblobgames.com/pathfinding/a-star/introduction.html)                    |

### 🎯 Missão da Semana: O Quebra-Cabeça (8-Puzzle)

Sua tarefa prática será implementar um agente capaz de resolver o clássico **Quebra-Cabeça de Blocos Deslizantes** (8-Puzzle).

O computador receberá o tabuleiro embaralhado e deverá nos dizer a sequência exata de movimentos para ordená-lo.

1. Crie seu repositório `treinamento-h2ia` (se ainda não criou).
2. Prepare seu ambiente Jupyter/Colab. Use [Modelo de Relatório.](https://colab.research.google.com/drive/1dQf8LOmDxFZFxQIOCO2MJDh_shXa-tnj?usp=sharing)
3. Tente implementar a estrutura de "Nó" e "Estado" conforme estudado.
4. Implemente (em ordem de dificuldade, vá até onde conseguir):

- Busca em profundidade
- Busca em largura
- Busca em profundidade com aprofundamento iterativo

5. Compare características, uso de memória, tempo de execução, comportamento, etc.

[Voltar para o início](./)

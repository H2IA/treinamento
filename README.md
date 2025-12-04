# Treinamento H2IA

O presente material serve como base de estudos e aprofundamento para o treinamento do Hub2IA @ UFPel.

## Semana 1 - Boas Vindas

Nesta primeira semana iremos apresentar o projeto Hub2IA bem como introduzir a área para novos alunos.

## Semana 2 - Colab e Ferramentas

Nesta semana fornecemos um notebook python para que vocês pudessem começar a experimentar o ambiente de notebooks, o colab e começar a mexer com python e algumas ferramentar comumente utilizadas.

A ideia é que seja algo bem introdutório e breve. Iremos aprofundar esses conhecimentos nas semanas seguintes.

## Semana 3 - Apresentação de Trabalhos do Hub2IA

Nesta semana iremos apresentar as pesquisas realizadas no Hub2IA e os pesquisadores que irão participar da organização do treinamento nesta edição.

Iremos também indicar o formato do treinamento e o que esperamos dos alunos.

---

## Semana 4 - Buscas

![Alt image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*VM84VPcCQe0gSy44l9S5yA.jpeg)
_Imagem retirada de [Breaking Down Breadh-First Search](https://medium.com/basecs/breaking-down-breadth-first-search-cebe696709d9)_

Nesta semana, iremos começar as implementações e de fato dar o ponta-pé inicial. Começaremos introduzindo conceitos da inteligência artificial clássica.

**Você já parou pra pensar:**

- Como o **Google Maps** ou **Waze** encontram o caminho mais curto entre a sua casa e a faculdade com incontáveis caminhos a serem percorridos?
- Como uma IA de xadrez decide a próxima jogada analisando milhões de possibilidades?
- Como um robô aspirador sabe como sair de um quarto sem bater nas paredes?

Nesta semana iremos aprender um assunto que parece um pouco distante do que esperamos do hype da IA, mas de extrema importância e que resolve e auxilia em diversos problemas como os supracitados.

### 📅 Roteiro de Estudos

Para que o nosso encontro prático seja produtivo, precisamos que você entenda a lógica antes de codar. Siga o roteiro abaixo:

#### 1. O Conceito Fundamental

Antes de sair buscando, precisamos saber **representar** o problema. Em IA, transformamos o mundo em **Estados** e **Ações**.

- **Leitura Importante:** [Representação de Problemas e Espaço de Estados](INSERIR_LINK_AQUI)
  - _Foco:_ Entenda o que é Estado Inicial, Estado Meta e Função Sucessora.

#### 2. Os Algoritmos (O "Como")

Vamos focar em duas estratégias clássicas de "Busca sem Informação" (ou Busca Cega):

- **Busca em Largura (BFS):** O algoritmo cauteloso que olha tudo ao redor antes de ir fundo. Garante o menor caminho (em grafos não ponderados), mas gasta muita memória.
- **Busca em Profundidade (DFS):** O algoritmo aventureiro que vai o mais longe possível em um caminho e só volta se der de cara com a parede. Gasta pouca memória, mas pode se perder ou não achar o melhor caminho.

### 📚 Material de Apoio

Reunimos os melhores materiais para você dominar o assunto:

| Tipo | Tópico         | Descrição                                        |        Link         |
| :--: | -------------- | ------------------------------------------------ | :-----------------: |
|  📄  | **Conceito**   | Introdução a Agentes e Ambientes                 |   [Ler Artigo](#)   |
|  🎥  | **BFS**        | Como funciona a Busca em Largura (Visualização)  | [Assistir Vídeo](#) |
|  🎥  | **DFS**        | Como funciona a Busca em Profundidade            | [Assistir Vídeo](#) |
|  📘  | **Referência** | Capítulo do Livro Norvig (Buscas Não Informadas) |    [Acessar](#)     |

### 🎯 Missão da Semana: O Quebra-Cabeça (8-Puzzle)

Sua tarefa prática será implementar um agente capaz de resolver o clássico **Quebra-Cabeça de Blocos Deslizantes** (8-Puzzle).

O computador receberá o tabuleiro embaralhado e deverá nos dizer a sequência exata de movimentos para ordená-lo.

1. Crie seu repositório `treinamento-h2ia` (se ainda não criou).
2. Prepare seu ambiente Jupyter/Colab.
3. Tente implementar a estrutura de "Nó" e "Estado" conforme estudado.
4. Implemente **DEFINIR O QUE IMPLEMENTAR**

### 📞 Dúvidas?

Utilizem nosso canal de discussões da semana para que possamos tirar as suas dúvidas e outros colegas possam acompanhar e interagir também. Ensinar outros também é aprender a generalizar e consolidar o conhecimento, portanto se encontrarem dúvidas que consigam auxiliar, aproveitem a oportunidade.

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

Para que o nosso encontro prático seja produtivo, precisamos que você entenda a lógica antes de codar. Siga o roteiro abaixo:

#### 1. O Conceito Fundamental

Antes de sair buscando, precisamos saber **representar** o problema. Em IA, transformamos o mundo em **Estados** e **Ações**.

- **Leitura Importante:** [Representação de Problemas e Espaço de Estados](INSERIR_LINK_AQUI)
  - _Foco:_ Entenda o que é Estado Inicial, Estado Meta e Função Sucessora.


#### 2. Os Algoritmos (O "Como")

Começaremos com duas estratégias clássicas de "Busca sem Informação" (ou Busca Cega):

- **Busca em Largura (BFS):** O algoritmo cauteloso que olha tudo ao redor antes de ir fundo. Garante o menor caminho (em grafos não ponderados), mas gasta muita memória.
- **Busca em Profundidade (DFS):** O algoritmo aventureiro que vai o mais longe possível em um caminho e só volta se der de cara com a parede. Gasta pouca memória, mas pode se perder ou não achar o melhor caminho.

### 📚 Material de Apoio

Reunimos os melhores materiais para você dominar o assunto:

**Leituras**

| Tipo | Tópico | Descrição | Link |
| :--: | :--- | :--- | :--: |
| 📄 | **Representação** | Representação e problem solving | [Acessar](https://drive.google.com/file/d/150sue3u4TUUaudYdEehR28kJAFmQEHON/view?usp=sharing) |
| 📄 | **Buscas** | Buscas - Resumido (Ricardo) | [Acessar](https://ricardomatsumura.medium.com/algoritmos-de-busca-para-intelig%C3%AAncia-artificial-7cb81172396c) |
| 🎥 | **Representação** | Representação do Conhecimento | [Assistir Vídeo](https://www.youtube.com/watch?v=V-O-RFSRe-E) |
| 🎥 | **BFS** | Como funciona a Busca em Largura | [Assistir Vídeo](https://www.youtube.com/watch?v=KiCBXu4P-2Y) |
| 🎥 | **DFS** | Como funciona a Busca em Profundidade | [Assistir Vídeo](https://www.youtube.com/watch?v=7fujbpJ0LB4) |
| 📘 | **Referência** | Capítulo do Livro Norvig (Buscas Não Informadas) | [Acessar](https://drive.google.com/file/d/1c_dFxt3KONbV7Z-r5Cr0smG8siCAe3le/view?usp=sharing) |

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


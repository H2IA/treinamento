---
layout: default
title: Semana 5 - Buscas Com Informação
---

# Semana 5 - Buscas Com Informação

![A* Pathfinding](https://www.redblobgames.com/pathfinding/a-star/a-star-tradeoffs.png)
_Imagem retirada de [Red Blob Games - Introduction to A*](https://www.redblobgames.com/pathfinding/a-star/introduction.html)_

Na semana passada exploramos as **Buscas Sem Informação** (BFS, DFS e aprofundamento iterativo). Vimos que esses algoritmos funcionam, mas exploram o espaço de estados "às cegas", sem nenhuma pista sobre o quão perto estão da solução.

Nesta semana damos o próximo passo: e se o nosso agente tivesse uma **intuição** que o ajudasse a decidir por onde ir primeiro? É exatamente essa a ideia da **Busca Com Informação** (ou busca informada).

**Você já parou pra pensar:**

- Ao procurar um endereço numa cidade nova, você caminha em qualquer direção ou tende a ir para o lado onde *acha* que o destino está?
- Como o **GPS** consegue traçar uma rota boa sem testar literalmente todos os caminhos possíveis do mapa?

A resposta está no uso de **heurísticas**: estimativas que guiam a busca em direção ao objetivo, tornando-a muito mais eficiente.

## 🧭 Conteúdo da Semana

De forma breve, os conceitos centrais desta semana são:

- **Heurística `h(n)`** — uma função que *estima* o custo restante de um estado até o objetivo. Ela não precisa ser exata, apenas uma boa "aposta" que oriente a exploração (ex.: distância em linha reta até o destino).
- **Busca Gulosa (Greedy Search)** — expande sempre o estado que *parece* mais próximo do objetivo, ou seja, aquele com menor `h(n)`. É rápida, mas pode se enganar e não garante o melhor caminho.
- **Algoritmo A\*** — combina o **custo já percorrido** `g(n)` com a **estimativa do que falta** `h(n)`, escolhendo o estado com menor `f(n) = g(n) + h(n)`. Com uma boa heurística, o A\* encontra o caminho ótimo de forma eficiente, unindo o melhor da busca gulosa com as garantias das buscas sem informação.

> A principal diferença entre a **Busca Gulosa** e o **A\*** é justamente o `g(n)`: a gulosa olha só para a estimativa do futuro; o A\* também leva em conta o caminho que já foi feito.

Os detalhes, exemplos visuais e a formalização de cada algoritmo estão nos **slides da aula** (link na tabela abaixo). Recomendamos acompanhá-los junto com os materiais de apoio.

### 📚 Material de Apoio

| Tipo | Tópico                    | Descrição                                                                                                  |                                                       Link                                                        |
| :--: | :------------------------ | :-------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------: |
|  📊  | **Slides da Aula**        | **Buscas Com Informação:** material apresentado no encontro, com heurística, Busca Gulosa e A\*.           |    [Acessar](https://docs.google.com/presentation/d/1gQBiVvTEjgxpcvZoT_5FTiXrYjlmtFBunQxXGeUf4JM/edit?usp=sharing)    |
|  🎮  | **Algoritmos Interativo** | **Red Blob Games:** visualize e compare Busca Gulosa e A\* interativamente e veja como a heurística guia a busca. |                   [Acessar](https://www.redblobgames.com/pathfinding/a-star/introduction.html)                    |
|  🎥  | **Conceito Visual**       | **CS50 - Search (Harvard):** revisão de buscas informadas, heurísticas e A\* (continuação da semana passada). |                              [Assistir](https://www.youtube.com/watch?v=WbzNRTTrX0g)                              |
|  📘  | **Referência**            | **Capítulo 3 - Russell & Norvig:** para quem quer o rigor matemático de heurísticas e A\* (Opcional/Consulta). |           [Acessar](https://drive.google.com/file/d/1c_dFxt3KONbV7Z-r5Cr0smG8siCAe3le/view?usp=sharing)           |

### 🎯 Missão da Semana: Resolvendo o 8-Puzzle com A\*

Na semana passada você atacou o **8-Puzzle** com buscas sem informação. Agora sua missão é resolver o **mesmo problema** usando **Busca Com Informação**, implementando o algoritmo **A\*** e comparando os resultados.

O tabuleiro é uma grade 3×3 com oito peças numeradas e um espaço vazio (`0`). O objetivo é ordená-lo até o estado alvo:

```
1 2 3
4 5 6
7 8 0
```

**Componentes a implementar (no Colab):**

1. **Representação do estado** — escolha a estrutura que preferir (lista, matriz, tupla...).
2. **Nó de busca** — deve guardar: o estado, `g(n)`, `h(n)`, `f(n)`, o nó pai e o movimento que o gerou (para reconstruir o caminho no final).
3. **Geração de sucessores** — localize o `0`, identifique os movimentos válidos (cima/baixo/esquerda/direita, sem sair do tabuleiro) e gere os novos estados.
4. **Custo `g(n)`** — número de movimentos desde o início; cada movimento custa 1, então `g(filho) = g(pai) + 1`.
5. **Heurística `h(n)`** — use a **Distância de Manhattan**: para cada peça, `|linha_atual - linha_objetivo| + |coluna_atual - coluna_objetivo|`, somada para todas as peças (o espaço vazio `0` **não** entra no cálculo).
6. **Avaliação `f(n) = g(n) + h(n)`** — lembre-se: o A\* expande o estado com menor `f(n)`, **não** o de menor `h(n)`. Essa é a diferença para a Busca Gulosa.

**Estruturas recomendadas:** uma **fila de prioridade** para a fronteira (*open list*, sempre expandindo o menor `f(n)`) e um **conjunto de visitados** (*closed list*) para não reexpandir estados repetidos.

**Ao final, exiba:**

- O estado final resolvido e o caminho (sequência de movimentos) encontrado;
- O número de movimentos da solução;
- A quantidade de estados expandidos;
- (Opcional) O tempo de execução.

**Compare com a semana anterior:** quantos estados o A\* expandiu em relação à BFS/DFS? O caminho encontrado foi ótimo? Reflita sobre o impacto da heurística na eficiência.

#### 🧩 Desafio Extra (Opcional): Solubilidade

Nem toda configuração do 8-Puzzle tem solução — algumas nunca alcançam o objetivo, faça o que fizer. Antes de rodar o A\*, implemente uma verificação que detecte se o estado inicial é solucionável e, se não for, avise e encerre. Pesquise sobre **número de inversões** e **paridade de estados**.

> **Reflexão:** qual a vantagem de checar a solubilidade antes de rodar o A\*? O que acontece com o tempo de execução ao tentar resolver um estado insolúvel? E em versões maiores, como o 15-Puzzle?

[Voltar para o início](./)

---
layout: default
title: Semana 5 - Buscas Com Informação
---

# Semana 5 - Buscas Com Informação

Na [semana 4](week-4.md), estudamos como explorar possibilidades usando fila e pilha. Essas estratégias conhecem os movimentos permitidos e sabem reconhecer o objetivo, mas não usam uma estimativa de quanto falta para chegar até ele.

Agora vamos acrescentar essa informação. No 8-puzzle, uma peça longe de sua posição final ainda terá de se mover. Podemos usar as distâncias das peças para estimar o trabalho restante e escolher quais possibilidades analisar primeiro.

## Antes de começar

Você precisa conseguir acompanhar uma busca pequena e explicar estado, nó, fronteira e caminho da solução. Se esses termos ainda se confundem, retome o exemplo da semana 4. Não é necessário ter concluído o aprofundamento iterativo para estudar esta parte.

## Roteiro de estudo

### 1. Construir uma estimativa

Abra a explicação interativa do Red Blob Games e acompanhe a comparação entre busca em largura, busca gulosa e A*. Observe quais posições cada estratégia analisa antes de chegar ao destino.

A função que estima o custo restante é chamada de **heurística**, escrita como `h(n)`. No 8-puzzle, vamos usar a distância de Manhattan: para cada peça numerada, conte quantas linhas e colunas a separam da posição correta e some os valores. O espaço vazio não entra nessa conta.

Por exemplo, se apenas a peça 8 estiver ao lado de sua posição final e puder entrar nela com uma jogada, a estimativa será 1. Em outros tabuleiros, as peças podem atrapalhar umas às outras: somar as distâncias não resolve o quebra-cabeça, apenas fornece um limite inferior para o número de movimentos necessários.

### 2. Comparar duas maneiras de usar a pista

A **busca gulosa** escolhe o nó com menor `h(n)`. Ela dá prioridade ao que parece mais próximo do objetivo. Isso pode reduzir bastante a exploração, mas também pode conduzir a um caminho ruim. Ela não garante o caminho mais curto nem é sempre mais rápida.

O **A\*** considera também o custo já percorrido, `g(n)`. Sua prioridade é `f(n) = g(n) + h(n)`. Se um nó tem `g=8` e `h=2`, sua prioridade é 10. Outro com `g=3` e `h=4` tem prioridade 7. A gulosa escolheria o primeiro; A* escolheria o segundo.

Acompanhe agora a parte de buscas informadas da aula “Search”, do CS50. Refaça uma comparação de prioridades antes de conferir a escolha do algoritmo. Os slides da aula podem ser usados depois como revisão.

### 3. Entender a garantia do A*

Para encontrar um caminho ótimo, não basta que a heurística pareça razoável. Uma heurística **admissível** nunca estima um custo maior que o mínimo realmente necessário. A distância de Manhattan tem essa propriedade no 8-puzzle com movimentos de custo 1: cada jogada desloca uma única peça numerada em uma casa.

Ela também é **consistente**: a estimativa antes de uma jogada não é maior que o custo dessa jogada somado à estimativa depois dela. Com essa propriedade e o tratamento correto dos custos, A* pode fechar um estado quando o retira da fila de prioridade, sem precisar expandi-lo novamente. A implementação deve reconhecer a solução quando o objetivo for retirado da fila, e não assim que ele aparecer entre os sucessores.

O capítulo de Russell e Norvig é a referência para aprofundar essas condições. Se você experimentar outra heurística, não presuma que ela mantém as mesmas garantias.

### Material de Apoio

| Tipo | Tópico                    | Descrição                                                                                                  |                                                       Link                                                        |
| :--: | :------------------------ | :-------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------: |
| Slides | **Slides da aula: Buscas** | Slides para acompanhar o estudo de buscas. | [Acessar](https://drive.google.com/file/d/1apKudeSNBhu1rGrKrG4B7cd-S2fhmwvN/view?usp=sharing) |
| Slides | **Slides complementares**        | **Buscas Com Informação:** material apresentado no encontro, com heurística, Busca Gulosa e A\*.           |    [Acessar](https://docs.google.com/presentation/d/1gQBiVvTEjgxpcvZoT_5FTiXrYjlmtFBunQxXGeUf4JM/edit?usp=sharing)    |
| Interativo | **Exemplo interativo** | **Red Blob Games:** visualize e compare Busca Gulosa e A\* interativamente e veja como a heurística guia a busca. |                   [Acessar](https://www.redblobgames.com/pathfinding/a-star/introduction.html)                    |
| Vídeo | **Conceito Visual**       | **CS50 - Search (Harvard):** revisão de buscas informadas, heurísticas e A\* (continuação da semana passada). |                              [Assistir](https://www.youtube.com/watch?v=WbzNRTTrX0g)                              |
| Livro | **Referência**            | **Capítulo 3 - Russell & Norvig:** para quem quer o rigor matemático de heurísticas e A\* (Opcional/Consulta). |           [Acessar](https://drive.google.com/file/d/1c_dFxt3KONbV7Z-r5Cr0smG8siCAe3le/view?usp=sharing)           |

### Atividade: Resolvendo o 8-Puzzle com A\*

A atividade usa o mesmo 8-puzzle da semana 4. Aproveite a representação do tabuleiro e a geração de movimentos para implementar A* e comparar os resultados. Se ainda não concluiu a atividade anterior, comece conferindo essas duas partes com um tabuleiro a uma jogada do objetivo.

O tabuleiro é uma grade 3×3 com oito peças numeradas e um espaço vazio (`0`). O objetivo é ordená-lo até o estado alvo:

```
1 2 3
4 5 6
7 8 0
```

**Componentes a implementar (no Colab):**

1. **Representação do estado**: escolha a estrutura que preferir (lista, matriz, tupla...).
2. **Nó de busca**: deve guardar: o estado, `g(n)`, `h(n)`, `f(n)`, o nó pai e o movimento que o gerou (para reconstruir o caminho no final).
3. **Geração de sucessores**: localize o `0`, identifique os movimentos válidos (cima/baixo/esquerda/direita, sem sair do tabuleiro) e gere os novos estados.
4. **Custo `g(n)`**: número de movimentos desde o início; cada movimento custa 1, então `g(filho) = g(pai) + 1`.
5. **Heurística `h(n)`**: use a **Distância de Manhattan**: para cada peça, `|linha_atual - linha_objetivo| + |coluna_atual - coluna_objetivo|`, somada para todas as peças (o espaço vazio `0` **não** entra no cálculo).
6. **Avaliação `f(n) = g(n) + h(n)`**: lembre-se: o A\* expande o estado com menor `f(n)`, **não** o de menor `h(n)`. Essa é a diferença para a Busca Gulosa.

Use uma **fila de prioridade** para a fronteira e guarde o menor custo `g` encontrado para cada estado. Se descobrir um caminho mais barato até um estado que ainda está na fronteira, atualize o custo e o caminho correspondente. Se a fila guardar entradas antigas, descarte-as quando forem retiradas.

Não marque um estado como encerrado só porque ele foi gerado. Com Manhattan neste problema, o conjunto de estados fechados deve registrar os que já foram retirados para expansão pelo menor `f`. Heurísticas admissíveis que não sejam consistentes podem exigir reabrir estados quando surgir um caminho melhor.

**Ao final, exiba:**

- O estado final resolvido e o caminho (sequência de movimentos) encontrado;
- O número de movimentos da solução;
- A quantidade de estados expandidos;
- (Opcional) O tempo de execução.

Compare BFS, DFS e A* nos mesmos tabuleiros. Comece por casos pequenos, em que a BFS consiga servir de referência para o menor número de movimentos. Registre também como desempata prioridades iguais; essa escolha pode alterar a quantidade de nós expandidos.

Antes de seguir, confira: você consegue calcular `g`, `h` e `f` de um nó e explicar qual deles a gulosa usa? Seu A* devolve um caminho válido com o mesmo comprimento da BFS nesses casos?

#### Desafio Extra (Opcional): Solubilidade

Nem toda configuração do 8-Puzzle tem solução: algumas nunca alcançam o objetivo, faça o que fizer. Antes de rodar o A\*, implemente uma verificação que detecte se o estado inicial é solucionável e, se não for, avise e encerre. Pesquise sobre **número de inversões** e **paridade de estados**.

> **Reflexão:** qual a vantagem de checar a solubilidade antes de rodar o A\*? O que acontece com o tempo de execução ao tentar resolver um estado insolúvel? E em versões maiores, como o 15-Puzzle?

### Como Entregar

Suba sua solução (o notebook `.ipynb` do Colab e quaisquer arquivos do trabalho) no seu repositório **`treinamento-h2ia`** no GitHub. Em seguida, envie o **link do repositório** através do formulário abaixo:

| Tipo | Descrição | Link |
| :--: | :-------- | :--: |
| Formulário | **Formulário de Entrega:** envie aqui o link do seu repositório no GitHub | [Enviar Trabalho](https://docs.google.com/forms/d/e/1FAIpQLSdhc2nfeByHE9Hkan-FIlmC1ZWm40Wy_p9QhDniECQWcVcvTA/viewform?usp=dialog) |

> Certifique-se de que o repositório esteja **público** (ou compartilhado) para que possamos acessá-lo, e que o notebook esteja salvo com as saídas das execuções visíveis.

[Voltar para o início](./)

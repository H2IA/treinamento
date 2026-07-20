---
layout: default
title: Semana 6 - Otimização e Metaheurísticas
---

# Semana 6 - Otimização e Metaheurísticas

Até aqui, nossas buscas tinham um objetivo claro: sair de um estado inicial e **chegar a um estado final** (o caminho no labirinto, o 8-Puzzle resolvido). Mas e quando não existe um "destino" definido — e sim uma **melhor configuração possível** entre um número gigantesco (às vezes infinito) de alternativas?

Nesta semana entramos no mundo da **otimização**: encontrar boas soluções **sem precisar testar todas as possibilidades**.

**Você já parou pra pensar:**

- Como um modelo de Machine Learning **ajusta seus parâmetros** para errar o mínimo possível?
- Como escolher os **melhores hiperparâmetros** de um modelo sem testar todas as combinações?
- Por que às vezes um algoritmo encontra uma solução "boa", mas não a **melhor** de todas?

A resposta passa por entender o espaço de busca como uma **paisagem de soluções** e navegar por ela de forma inteligente.

## 🧭 Conteúdo da Semana

De forma breve, os conceitos centrais desta semana são:

- **Problema de busca/otimização** — todo problema tem três peças: o **espaço de busca** (todas as soluções possíveis), a **função objetivo** (o critério que mede a qualidade de uma solução) e o **algoritmo** (a estratégia para navegar).
- **Mínimos local vs. global** — o cuidado central: *ser bom localmente não significa ser o melhor globalmente*. Muitos algoritmos ficam "presos" em vales secundários.
- **Exploration vs. Exploitation** — o dilema de todo método de busca: **explorar** regiões desconhecidas em busca de novas oportunidades, ou **aproveitar** (refinar) regiões que já parecem promissoras.
- **Metaheurísticas** — estratégias gerais para escapar de mínimos locais e navegar espaços difíceis:
  - **Hill Climbing** e **Random-Restart** (reinícios aleatórios);
  - **Simulated Annealing** (recozimento simulado, inspirado no resfriamento de metais);
  - **Tabu Search** (memória de soluções recém-visitadas);
  - **Algoritmos Genéticos** (populações que evoluem por seleção, crossover e mutação).

> Diferente das buscas anteriores, aqui geralmente **não há um caminho** a reconstruir — o que importa é a **qualidade da solução final** encontrada.

Os detalhes, as intuições visuais e a formalização de cada método estão nos **slides da aula** (link na tabela abaixo).

### 📚 Material de Apoio

| Tipo | Tópico | Descrição | Link |
| :--: | :----- | :-------- | :--: |
| 📊 | **Slides da Aula** | **Busca em Espaços (Thiago Reis Porto):** otimização, mínimos local/global, exploration vs. exploitation e metaheurísticas. | [Acessar](https://docs.google.com/presentation/d/1ioLN5dje44bmHv2cdeF7xFvfW_WKW2IFrJ7lxEj38pw/edit?usp=sharing) |

### 🎯 Missão da Semana: Otimizando a Função de Rastrigin

Sua missão é implementar **dois algoritmos de busca do zero** e usá-los para **minimizar** uma função conhecida por ser um "campo minado" de mínimos locais: a **Função de Rastrigin**.

**Regras do desafio:**

- Implemente **dois** algoritmos entre os vistos na aula (ex.: Hill Climbing, Random-Restart, Simulated Annealing, Tabu Search ou Algoritmo Genético).
- Escreva os algoritmos **do zero** — **sem** bibliotecas de otimização prontas (`scipy.optimize`, frameworks de GA, etc.) e **sem** auxílio de IA. O objetivo é entender o funcionamento na prática.
- Use `numpy` apenas para a matemática vetorial, se quiser.

**O problema — Função de Rastrigin:**

```
f(x) = 10·n + Σ [ xᵢ² − 10·cos(2π·xᵢ) ]   , para i = 1..n
```

- Domínio usual: cada `xᵢ ∈ [-5.12, 5.12]`.
- **Mínimo global:** `f(x) = 0` em `x = (0, 0, ..., 0)`.
- Trabalhe com **10 ou mais dimensões** (`n ≥ 10`). O termo do cosseno cria inúmeros mínimos locais, o que torna a otimização desafiadora e ótima para comparar estratégias.

**Ao final, apresente:**

- A melhor solução encontrada por cada algoritmo e o valor da função objetivo `f(x)`;
- O número de avaliações da função (ou iterações) até convergir;
- Uma **comparação** entre os dois métodos: quem chegou mais perto do mínimo global? Quem foi mais rápido? Como cada um lidou com o dilema *exploration vs. exploitation*?
- Reflita: o quanto o **ponto inicial** e os **parâmetros** (passo, temperatura, taxa de mutação, etc.) afetaram o resultado?

### 📤 Como Entregar

Suba sua solução (o notebook `.ipynb` do Colab e quaisquer arquivos) no seu repositório **`treinamento-h2ia`** no GitHub.

> 📌 O link do **formulário de entrega** será disponibilizado em breve aqui nesta página.

> 💡 Certifique-se de que o repositório esteja **público** (ou compartilhado) e que o notebook esteja salvo com as saídas das execuções visíveis.

[Voltar para o início](./)

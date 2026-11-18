---
layout: default
title: Semana 10 - Redes Neurais (MLP)
---

# Semana 10 - Redes Neurais (MLP)

Na semana passada, o modelo era uma soma de atributos multiplicados por pesos, e o gradiente descendente ajustava esses pesos dando pequenos passos contra o erro. Esta semana a gente empilha essa ideia: cada neurônio faz uma soma com pesos, passa o resultado por uma função de ativação e entrega a saída para a camada seguinte. Esse empilhamento é o **perceptron de múltiplas camadas**, a MLP.

Na aula, montamos uma MLP pequena, com 2 entradas, 4 neurônios ocultos e 3 saídas, e a usamos para classificar as flores do Iris pelo comprimento e pela largura da sépala. Vimos o **forward**, que leva a flor da entrada até a resposta; a **perda**, que mede o quanto a rede errou; e o **backpropagation**, que usa a regra da cadeia para descobrir a culpa de cada peso nesse erro. No fim, escrevemos tudo isso em poucas linhas de PyTorch.

## Material de apoio

Os materiais abaixo são para quem quiser aprofundar o estudo de redes neurais. Não é preciso ler tudo: comece pelos vídeos e use os livros quando quiser ver as contas com mais detalhe.

| Tipo | Material | Como usar |
| :--: | :-- | :-- |
| Vídeo | [3Blue1Brown](https://www.youtube.com/@3blue1brown), série *Neural networks* | Explica visualmente o que é uma rede neural, o gradiente descendente e o backpropagation. Um bom primeiro contato antes dos livros. Em inglês, com legendas. |
| Texto | [The Neural Network Zoo — Asimov Institute](https://www.asimovinstitute.org/neural-network-zoo/) | Um mapa ilustrado das principais arquiteturas de redes neurais. Mostra onde a MLP se encaixa entre as redes que vêm depois. Em inglês. |
| Livro | Ronald T. Kneusel, *Math for Deep Learning* (2021), capítulo 10, *Backpropagation* | Deriva o backpropagation passo a passo, com código. É o mais próximo do que fizemos em aula. Em inglês. |
| Livro | Ronald T. Kneusel, *Math for Deep Learning* (2021), capítulo 11, *Gradient Descent* | Retoma o gradiente descendente da semana passada e apresenta as variações usadas para treinar redes, como o Adam. Em inglês. |
| Livro | Simon Haykin, *Neural Networks: A Comprehensive Foundation*, 2ª edição (1999), capítulo 4, *Multilayer Perceptrons* | Referência clássica sobre a MLP e o backpropagation, com a derivação completa. Em inglês. |
| Livro | Simon Haykin, *Neural Networks and Learning Machines*, 3ª edição (2009), capítulo 4, *Multilayer Perceptrons* | Versão atualizada do capítulo anterior. Em inglês. |
| Livro | Christopher M. Bishop, *Pattern Recognition and Machine Learning* (2006), capítulo 5, *Neural Networks* | Tratamento mais matemático, que liga as redes neurais à regressão e à classificação que vimos nas semanas anteriores. Em inglês. |

## Atividade: construindo a MLP

A tarefa é reconstruir a rede neural da aula. O código dos slides está no notebook, mas algumas linhas foram apagadas: os pesos, o forward, a perda, os quatro tempos do passo de treino e a inferência. Você vai preencher essas lacunas e conferir cada uma com os números que calculamos em aula.

[Abra o notebook da atividade](https://colab.research.google.com/github/H2IA/treinamento/blob/main/notebooks/atividade-mlp.ipynb)

> **Antes de editar:** abra o notebook no Google Colaboratory e use **Arquivo → Salvar uma cópia no Drive**. Trabalhe na sua própria cópia para não perder as alterações.

O notebook está dividido assim:

1. **Os dados.** O Iris com as duas medidas da sépala, já separado em treino e teste. Esta parte está pronta.
2. **Os pesos.** As matrizes `W1` e `W2` e os vieses `b1` e `b2`.
3. **O forward.** A conta `z = tanh(x · W1 + b1)` e `s = z · W2 + b2`. Com os pesos da aula, o Exemplo 1 precisa dar os mesmos logits dos slides.
4. **A perda.** A entropia cruzada, primeiro à mão e depois com o PyTorch.
5. **O backpropagation, por dentro.** A derivada ∂E/∂w₁₁ calculada pelo PyTorch e pela regra da cadeia, que precisam dar o mesmo −4,37 da aula.
6. **O treino.** Os quatro tempos de cada passo: zerar as derivadas, forward e erro, backpropagation e ajuste dos pesos.
7. **A inferência.** A rede congelada, só com forward e argmax, e as fronteiras de decisão.
8. **Mexendo na rede.** O número de neurônios ocultos, a rede sem a tanh e a taxa de aprendizado.

Cada lacuna vem seguida de uma célula de conferência. Se ela falhar, volte à lacuna antes de seguir, porque as partes seguintes dependem dela.

### Como entregar

Entregue o notebook executado, com as saídas visíveis e as perguntas respondidas.

[Voltar para o início](./)

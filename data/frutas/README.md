# Dados da atividade das frutas

Os arquivos desta pasta foram adaptados da atividade **Distinguindo frutas**, usada por Ricardo Matsumura no material de Introdução ao Aprendizado de Máquina do H2IA.

- `train.csv`: 48 frutas com características e classe conhecida;
- `test.csv`: 11 frutas novas, sem a classe visível;
- `train_extended.csv`: as 48 frutas acima mais 8 exemplos sintéticos, usados na semana 8;
- `test_extended.csv`: as 11 frutas de `test.csv` mais 4 exemplos sintéticos;
- o gabarito do teste não fica no repositório enquanto a atividade estiver em andamento.

Os arquivos originais continuam válidos para a atividade da semana 7. Os arquivos `_extended` acrescentam duas classes sintéticas, `grapefruit` (toranja) e `lime` (lima), com poucos exemplos cada. O objetivo é tornar o conjunto desbalanceado, para que a atividade da semana 8 mostre a diferença entre acurácia e métricas por classe.

| Classe | `train.csv` | `train_extended.csv` |
| :-- | --: | --: |
| `orange` | 16 | 16 |
| `apple` | 15 | 15 |
| `lemon` | 13 | 13 |
| `grapefruit` | — | 5 |
| `mandarin` | 4 | 4 |
| `lime` | — | 3 |
| **total** | **48** | **56** |

Os valores sintéticos foram escolhidos à mão, mantendo faixas plausíveis para cada fruta. As toranjas ficam claramente acima das laranjas em massa e largura (418–496 g e 10,2–11,0 cm, contra 140–356 g e 6,7–9,2 cm), e as limas ocupam a faixa entre a tangerina e o limão pequeno, com cor um pouco mais baixa.

A separação folgada entre toranja e laranja é deliberada. Numa primeira versão as duas faixas quase se tocavam, e o resultado foi que uma laranja do teste caía dentro da faixa da toranja em dois atributos — um erro que não ensinava nada, porque vinha da construção dos dados e não do algoritmo. As sobreposições que restam, entre maçã, laranja e limão, são as do conjunto original.

Cada linha tem um identificador e quatro características:

| Coluna | Significado |
| :-- | :-- |
| `id` | identificador da fruta |
| `mass` | massa |
| `width` | largura |
| `height` | altura |
| `color_score` | medida numérica de cor |
| `fruit_name` | classe da fruta; aparece apenas em `train.csv` |

As classes originais são `apple`, `mandarin`, `orange` e `lemon`. Na atividade, `mandarin` é apresentada como tangerina.

Fonte de referência: [planilha original da atividade](https://docs.google.com/spreadsheets/d/1gMicTNBt_He-dAbxYTRAsibnzqIMb7x-063j7Py_-fg/edit?gid=0#gid=0).

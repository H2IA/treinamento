# Dados da atividade das frutas

Os arquivos desta pasta foram adaptados da atividade **Distinguindo frutas**, usada por Ricardo Matsumura no material de Introdução ao Aprendizado de Máquina do H2IA.

- `train.csv`: 48 frutas com características e classe conhecida;
- `test.csv`: 11 frutas novas, sem a classe visível;
- o gabarito do teste não fica no repositório enquanto a atividade estiver em andamento.

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

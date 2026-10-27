# Dados da atividade de diabetes

Os arquivos desta pasta vêm do conjunto **Diabetes** distribuído com o scikit-learn, na versão sem padronização (`load_diabetes(scaled=False)`). Os dados foram coletados para o artigo de Efron, Hastie, Johnstone e Tibshirani (2004) e descrevem 442 pacientes com diabetes.

- `train.csv`: 354 pacientes, com as medidas e a progressão conhecida;
- `test.csv`: 88 pacientes, sem a coluna `progression`;
- o gabarito do teste não fica no repositório enquanto a atividade estiver em andamento.

A divisão entre treino e teste foi sorteada uma única vez, com `numpy.random.default_rng(9)`, separando 88 pacientes para o teste. O conjunto original é público, então o gabarito pode ser reconstruído por quem procurar. A regra da atividade é não fazer isso antes de congelar o modelo.

Cada linha tem um identificador, dez medidas tomadas no início do acompanhamento e a resposta:

| Coluna | Significado |
| :-- | :-- |
| `id` | identificador do paciente, na ordem do conjunto original |
| `age` | idade, em anos |
| `sex` | sexo, codificado como 1 ou 2 |
| `bmi` | índice de massa corporal (IMC) |
| `bp` | pressão arterial média |
| `s1` | colesterol total (TC) |
| `s2` | lipoproteínas de baixa densidade (LDL) |
| `s3` | lipoproteínas de alta densidade (HDL) |
| `s4` | razão entre colesterol total e HDL (TCH) |
| `s5` | provavelmente o logaritmo dos triglicerídeos (LTG) |
| `s6` | glicemia (GLU) |
| `progression` | medida quantitativa da progressão da doença um ano depois; aparece apenas em `train.csv` |

A documentação original não informa qual valor de `sex` corresponde a cada sexo, nem a escala exata de `progression`. Para a atividade isso não importa: o objetivo é estudar o modelo, não tirar conclusões clínicas.

Fontes: [descrição no scikit-learn](https://scikit-learn.org/stable/datasets/toy_dataset.html#diabetes-dataset), [página dos dados originais](https://www4.stat.ncsu.edu/~boos/var.select/diabetes.html) e [Efron et al., *Least Angle Regression*](https://web.stanford.edu/~hastie/Papers/LARS/LeastAngle_2002.pdf).

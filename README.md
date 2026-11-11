# CitizenTech — Vai chover na próxima hora em São Paulo?

Projeto de Inteligência Artificial & Machine Learning — Global Solution FIAP 2026.

Modelo de **Random Forest** que estima, com as medições oficiais da estação **INMET A701 (São Paulo/Mirante de Santana)**, a probabilidade de chover na próxima hora — base para um aviso de curtíssimo prazo ao cidadão.

## Equipe

- Albert Katri, RM556544, `0ldev`
- Bruno Biletsky, RM554739, `Bruno-Biletsky`
- Paulo Akira, RM556840, `pauloakira05`

## Entregáveis

| Entregável | Local |
|---|---|
| Notebook executado (dados → preparação → treino → avaliação → conclusão) | [`ml/projeto_chuva_sp.ipynb`](ml/projeto_chuva_sp.ipynb) |
| Fonte, link, período e variáveis dos dados | [`ml/dados/README.md`](ml/dados/README.md) |
| Dados brutos oficiais do INMET (2023–2025) | [`ml/dados/brutos/`](ml/dados/brutos/) |
| Dependências | [`ml/requirements.txt`](ml/requirements.txt) (cópia em [`requirements.txt`](requirements.txt)) |
| Relatório | [`RELATORIO_ML.md`](RELATORIO_ML.md) |
| Vídeo (até 5 min, YouTube não listado) | _link do vídeo aqui_ |

## Resultado em uma linha

Teste em 2025 (ano inteiro nunca visto no treino): **F1 0,59 · recall 0,66 · ROC-AUC 0,93** para a classe chuva; o modelo avisa 65,6 % das horas de chuva com 1 h de antecedência (persistência: 57,5 %) e antecipa 19,6 % dos **inícios** de chuva, que a regra de persistência nunca prevê.

## Integração futura com o PONTOVOZ (ponto inteligente)

As previsões deste modelo poderão ser integradas ao **PONTOVOZ**, o nosso ponto de ônibus inteligente, para transformar a probabilidade de chuva em informação útil para quem está esperando o transporte:

- **Ônibus que podem atrasar:** quando o modelo indicar chuva na próxima hora, o PONTOVOZ avisa quais linhas que passam naquele ponto têm maior risco de atraso (por exemplo, linhas que cruzam vias com histórico de alagamento ou trânsito lento sob chuva).
- **Alerta de chuva ao usuário:** se a chuva for provável, o ponto avisa o usuário com antecedência para que ele tome a melhor decisão — por exemplo, seguir para uma estação de metrô próxima em vez de esperar um ônibus que pode atrasar, ou se abrigar antes de a chuva começar.

Assim, o aviso de curtíssimo prazo deixa de ser apenas uma previsão do tempo e passa a apoiar decisões de mobilidade no momento em que o cidadão mais precisa.

## Como executar

Requer Python 3.10+ (testado com Python 3.13). Os dados estão no repositório: **não é preciso internet**.

```bash
python -m pip install -r ml/requirements.txt
cd ml
python -m jupyter notebook projeto_chuva_sp.ipynb
```

Ou, para reexecutar tudo de uma vez pela linha de comando (≈ 1–2 min):

```bash
cd ml
python -m jupyter nbconvert --to notebook --execute --inplace projeto_chuva_sp.ipynb
```

O resultado é reprodutível (`random_state=42`, dados versionados).

## Estrutura

```
.
├── README.md
├── RELATORIO_ML.md
├── requirements.txt
└── ml/
    ├── projeto_chuva_sp.ipynb
    ├── requirements.txt
    ├── figuras/            # gráficos gerados pelo notebook (usados no relatório)
    └── dados/
        ├── README.md
        └── brutos/         # CSVs oficiais INMET A701 2023, 2024, 2025
```

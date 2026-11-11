# Dados

Dados **reais e públicos** do Instituto Nacional de Meteorologia (INMET). Nenhum dado simulado ou sintético foi usado.

| Item | Valor |
|---|---|
| Fonte | INMET — Banco de Dados Meteorológicos, *Dados Históricos Anuais* das estações automáticas |
| Link (página) | https://portal.inmet.gov.br/dadoshistoricos |
| Links (arquivos) | https://portal.inmet.gov.br/uploads/dadoshistoricos/2023.zip · [2024.zip](https://portal.inmet.gov.br/uploads/dadoshistoricos/2024.zip) · [2025.zip](https://portal.inmet.gov.br/uploads/dadoshistoricos/2025.zip) |
| Estação | **A701 — São Paulo / Mirante de Santana** (SP) |
| Coordenadas | lat −23,4964 · lon −46,6200 · altitude 785,6 m |
| Período | **01/01/2023 a 31/12/2025** (3 anos, 26.304 registros horários) |
| Frequência | horária (hora UTC, convertida para horário de Brasília no notebook) |
| Download | 06/11/2026 |
| Licença / uso | dados públicos do governo federal, livre uso com citação da fonte |

## Arquivos

`brutos/` contém os CSVs **exatamente como publicados pelo INMET**, apenas extraídos do `.zip` anual de cada ano e renomeados:

| Arquivo no repositório | Nome original no `.zip` |
|---|---|
| `INMET_A701_SAO_PAULO_MIRANTE_2023.CSV` | `INMET_SE_SP_A701_SAO PAULO - MIRANTE_01-01-2023_A_31-12-2023.CSV` |
| `INMET_A701_SAO_PAULO_MIRANTE_2024.CSV` | `INMET_SE_SP_A701_SAO PAULO - MIRANTE_01-01-2024_A_31-12-2024.CSV` |
| `INMET_A701_SAO_PAULO_MIRANTE_2025.CSV` | `INMET_SE_SP_A701_SAO PAULO - MIRANTE_01-01-2025_A_31-12-2025.CSV` |

Formato: separador `;`, decimal `,`, codificação Latin-1, 8 linhas de metadados da estação antes do cabeçalho. Falhas do sensor aparecem como `-9999` ou célula vazia.

Os arquivos ficam versionados para que o notebook rode **sem internet** e com resultado reproduzível. Para conferir a origem, basta baixar os `.zip` acima e comparar.

## Variáveis usadas

| Coluna original (INMET) | Nome no notebook | Unidade |
|---|---|---|
| PRECIPITAÇÃO TOTAL, HORÁRIO | `precipitacao_mm` (também define o alvo) | mm |
| PRESSAO ATMOSFERICA AO NIVEL DA ESTACAO, HORARIA | `pressao_hpa` | hPa (mB) |
| RADIACAO GLOBAL | `radiacao_kj_m2` | kJ/m² |
| TEMPERATURA DO AR - BULBO SECO, HORARIA | `temperatura_c` | °C |
| TEMPERATURA DO PONTO DE ORVALHO | `ponto_orvalho_c` | °C |
| UMIDADE RELATIVA DO AR, HORARIA | `umidade_pct` | % |
| VENTO, DIREÇÃO HORARIA | `vento_direcao_graus` | graus |
| VENTO, RAJADA MAXIMA | `vento_rajada_ms` | m/s |
| VENTO, VELOCIDADE HORARIA | `vento_velocidade_ms` | m/s |

## Qualidade observada

- Precipitação faltante em 2,7 % das horas; demais sensores ≈ 1,1 %.
- Radiação global vazia em 46,8 % das horas (o INMET não registra radiação à noite → tratada como 0 no período noturno).
- Nenhum timestamp duplicado e nenhuma hora ausente na grade; nenhum valor fora das faixas físicas verificadas.
- Após a limpeza, 25.024 das 26.304 horas (95,1 %) foram aproveitadas.

Alvo: `chuva_prox_hora` = 1 quando a precipitação da hora seguinte é > 0 mm (resolução do pluviômetro: 0,2 mm). Ocorre em 7,4 % das horas.

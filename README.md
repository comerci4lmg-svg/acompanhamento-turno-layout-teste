# Acompanhamento de Turnos GO

Aplicativo Streamlit que apresenta os turnos das equipes GOOL, GOOC, GOOK e GOOH.
Os dados são consultados por meio do Google Apps Script conectado à planilha
`acompanha turnos`.

O aplicativo inclui a tabela detalhada, o mapa mensal colorido de presença, a tabela
mensal de horas trabalhadas, a tabela mensal de intervalos, o ranking de maiores
intervalos individuais e o resumo diário. Registros da mesma equipe no mesmo dia são
consolidados em um único turno: primeira abertura, último fechamento e soma dos
intervalos oficiais associados a todos esses registros. Datas e horários são exibidos
no fuso `America/Sao_Paulo`.

As horas trabalhadas correspondem ao período entre a primeira abertura e o último
fechamento do dia. O tempo de intervalo é acompanhado em uma tabela separada e não é
descontado das horas trabalhadas.
Valores de horas iguais a `00:00` são exibidos como `-`, com fundo branco.
Na tabela mensal, jornadas abaixo de `06:00` ficam roxas, jornadas de `06:00` até
`07:59` ficam vermelhas e jornadas a partir de `08:00` ficam verdes.

O tempo de intervalo e seu motivo vêm das tabelas oficiais
`EQTLINFO_RAW.OPER_GO.INTERVALO` e `EQTLINFO_RAW.OPER_GO.MOTIVO_INTERVALO`, ligadas ao
turno por `HIST_TURMA_PLANTAO_ID`.
O ranking mantém cada `INTERVALO_ID` separado e apresenta equipe, início, fim, duração
e motivo, em ordem decrescente de duração. Ele é dividido em três tabelas com
classificações independentes: refeição, manutenção no veículo e retorno para a base.
Na tabela mensal de intervalos, valores abaixo de `01:00`, inclusive `00:00`, ficam
laranjas; de `01:00` até `01:15` ficam verdes; de `01:16` até `02:30` ficam
vermelhos; acima de `02:30` ficam roxos; e dias sem turno ficam com fundo branco.


As equipes `GOOH013M`, `GOOL007M`, `GOOL021M`, `GOOL024M`, `GOOL025M`, `GOOK013M`,
`GOOK012M` e `GOOK010M` são tratadas como desmobilizadas: ficam ocultas nas matrizes
quando não registram abertura no mês selecionado e reaparecem automaticamente quando
possuem movimento.

## Publicação no Streamlit Community Cloud

Use `streamlit_app.py` como arquivo principal.

Em **App settings → Secrets**, configure:

```toml
[apps_script]
url = "URL_FINAL_DO_APPS_SCRIPT_TERMINADA_EM_EXEC"
read_token = "READ_TOKEN_CONFIGURADO_NO_APPS_SCRIPT"
```

O arquivo real `.streamlit/secrets.toml` não deve ser enviado ao GitHub.

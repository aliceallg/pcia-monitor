# pcia-monitor

Vigia público e simples da plataforma Prosperando com IA. A cada 10 minutos ele abre cinco endereços públicos da plataforma e, se algum não responder o esperado duas vezes seguidas, abre uma issue "FORA DO AR" neste repositório. Quando tudo volta, comenta e fecha a issue sozinho.

Este repositório tem só o arquivo `.github/workflows/monitor.yml` e este texto. Não guarda segredo, token, dado de pessoa nem código da plataforma, e o fluxo não usa ação de terceiros.

## O que ele confere

| Endereço                        | Resposta esperada |
| ------------------------------- | ----------------- |
| `/entrar`, `/inicio`, `/termos` | 200               |
| `/api/ai/status` (sem login)    | 401               |
| `/api/health` (banco e Auth)    | 200               |

Cada endereço tem 10 segundos para responder. Se alguma verificação falhar, o monitor espera 30 segundos e tenta de novo. Uma falha repetida deixa a execução em vermelho e abre o alerta. Se já houver um alerta aberto, o monitor comenta no máximo uma vez por hora.

## Mudar o endereço ou pausar

Em Settings > Secrets and variables > Actions > Variables:

- `MONITOR_BASE_URL` define o endereço-base com `https://`, sem barra no fim, espaços ou quebras de linha. O valor padrão é `https://prosperando.aliceallgayer.com.br`.
- `MONITOR_PAUSADO`: `true` pausa o monitor (manutenção). Apagar a variável religa.

## Desligar

Aba Actions, "Monitor da plataforma", "Disable workflow". Definitivo: apagar o arquivo ou o repositório.

## Limites

O agendamento do GitHub às vezes atrasa alguns minutos e é desligado depois de 60 dias sem atividade no repositório (chega um e-mail; basta reativar). As issues deste repositório são públicas.

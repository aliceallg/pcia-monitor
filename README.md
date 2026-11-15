# pcia-monitor

Vigia público e simples da plataforma Prosperando com IA. A cada 10 minutos ele abre quatro endereços públicos da plataforma e, se algum não responder o esperado duas vezes seguidas, abre uma issue "FORA DO AR" neste repositório. Quando tudo volta, comenta e fecha a issue sozinho.

Este repositório tem só o arquivo `.github/workflows/monitor.yml` e este texto. Não guarda segredo, token, dado de pessoa nem código da plataforma, e o fluxo não usa ação de terceiros.

## O que ele confere

| Endereço                        | Resposta esperada |
| ------------------------------- | ----------------- |
| `/entrar`, `/inicio`, `/termos` | 200               |
| `/api/ai/status` (sem login)    | 401               |

Cada endereço tem 10 segundos para responder. Falhou: espera 30 segundos e tenta de novo. Falhou de novo: abre a issue (ou, se já houver uma aberta, comenta no máximo uma vez por hora).

## Mudar o endereço ou pausar

Em Settings > Secrets and variables > Actions > Variables:

- `MONITOR_BASE_URL`: endereço-base, com `https://`, sem barra no fim e sem espaço nem quebra de linha (ex.: `https://prosperando.aliceallgayer.com.br`). Sem ela vale o endereço da Vercel que está no arquivo.
- `MONITOR_PAUSADO`: `true` pausa o monitor (manutenção). Apagar a variável religa.

## Desligar

Aba Actions, "Monitor da plataforma", "Disable workflow". Definitivo: apagar o arquivo ou o repositório.

## Limites

O agendamento do GitHub às vezes atrasa alguns minutos e é desligado depois de 60 dias sem atividade no repositório (chega um e-mail; basta reativar). As issues deste repositório são públicas.

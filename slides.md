---
theme: dracula
highlighter: shiki
author: edsoncelio
title: 'Observabilidade 101'
mdc: true
transition: slide-left
hideInToc: true
---

# Observabilidade 101

Tudo (ou quase tudo) que você precisa saber sobre o assunto :)

<br>

<!-- ![Chiquinha - "posso fazer uma observação?"](https://i.makeagif.com/media/4-17-2017/RxTDJa.gif) -->

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/edsoncelio/talks" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---
layout: author
hideInToc: true
---

![profile-pic](https://github.com/edsoncelio.png?size=100)

# Edson Ferreira

SRE, Mantenedor da [documentação do Kubernetes](https://kubernetes.io/docs/pt) e do [Glossário da CNCF](https://glossary.cncf.io/pt-br) em Português e 
nas horas vagas escreve uns códigos na linguagem da Marmota (Golang ❤️)

<footer>

[twitter.com/@tuxpilgrim](https://twitter.com/tuxpilgrim)
[github.com/edsoncelio](https://github.com/edsoncelio)
[edsoncelio.dev](https://edsoncelio.dev)

</footer>

---
transition: slide-left
hideInToc: true
---

# Agenda

<Toc minDepth="1" maxDepth="2"></Toc>

---
transition: slide-left
layout: fact
level: 1
hideInToc: true
---

# "Hope is not a strategy."

[Traditional SRE saying](https://sre.google/sre-book/introduction/)

---
transition: slide-left
layout: section
level: 1
---

# O Que é Observabilidade?

---
transition: slide-left
layout: quote
level: 1
hideInToc: true
---

"Observabilidade é a capacidade de compreender o estado interno de um sistema examinando suas saídas. No contexto do software, isso significa ser capaz de compreender o estado interno de um sistema examinando seus dados de telemetria, que incluem rastros, métricas e logs ."

"Para tornar um sistema observável, ele deve ser instrumentado. Ou seja, o código deve emitir rastros, métricas ou logs. Os dados instrumentados devem então ser enviados para um backend de observabilidade."

---
transition: slide-left
layout: section
level: 1
---

# Pilares da Observabilidade

---
transition: slide-left
level: 2
---

# Logs

Um log é um registro de texto com marcação de data/hora, estruturado (recomendado) ou não estruturado, com metadados. De todos os sinais de telemetria, os logs são os que têm o maior legado. A maioria das linguagens de programação possui bibliotecas de logging de forma nativa.

<br>

```bash
I, [2021-02-23T13:26:23.505892 #22473]  INFO -- : [6459ffe1-ea53-4044-aaa3-bf902868f730] Started GET "/" for ::1 at 2021-02-23 13:26:23 -0800
```

---
transition: slide-left
level: 2
---

# Métricas

Uma métrica é uma medida de um serviço capturado em tempo de execução. O momento de captura de uma medida é conhecido como evento métrico, que consiste não apenas na medida em si, mas também no momento em que ela foi capturada e nos metadados associados.

<br>

```bash
avg(rate(node_cpu{job="default/node-exporter",mode="idle"}[1m]))
```
---
transition: slide-left
level: 2
---

# Rastros (traces)

Os rastreamentos nos dão uma visão geral do que acontece quando uma solicitação é feita a uma aplicação. Quer seu aplicativo seja um monólito com um único banco de dados ou uma rede mesh sofisticada de serviços, os rastreamentos são essenciais para entender o “caminho” completo que uma solicitação percorre na sua aplicação.

## Spans 
A span represents a unit of work or operation. Spans are the building blocks of Traces.

```json {maxHeight:'100px'}
{
  "name": "hallo",
  "context": {
    "trace_id": "0x5b8aa5a2d2c872e8321cf37308d69df2",
    "span_id": "0x051581bf3cb55c13"
  },
  "start_time": "2022-04-29T18:52:58.114201Z",
  "end_time": "2022-04-29T18:52:58.114687Z",
  "events": [
    {
      "name": "Guten Morgen!",
      "timestamp": "2022-04-29T18:52:58.114561Z",
    }
  ]
}

```

---
transition: slide-left
level: 1
---

# Metodologias de Monitoramento
- RED
- USE
- The Four Golden Signals

---
transition: slide-left
level: 1
---

# Projeto OpenTelemetry (OTEL)
OpenTelemetry satisfies the need for observability while following two key principles:

- You own the data that you generate. There’s no vendor lock-in.
- You only have to learn a single set of APIs and conventions.

---
transition: slide-left
hideInToc: true
level: 1
---

## Componentes do OpenTelemetry (OTEL)

<br>

- A specification for all components
- A standard protocol that defines the shape of telemetry data
- Semantic conventions that define a standard naming scheme for common telemetry data types
- APIs that define how to generate telemetry data
- Language SDKs that implement the specification, APIs, and export of telemetry data
- A library ecosystem that implements instrumentation for common libraries and frameworks
- Automatic instrumentation components that generate telemetry data without requiring code changes
- The OpenTelemetry Collector, a proxy that receives, processes, and exports telemetry data
- Various other tools, such as the OpenTelemetry Operator for Kubernetes, OpenTelemetry Helm Charts, and community assets for FaaS

---
transition: slide-left
layout: section
level: 1
---

# Stack da Grafana Labs

---
transition: slide-left
hideInToc: true
level: 3
---

# Loki
Indexador de logs, faz parte da stack opensource da Grafana Labs

---
transition: slide-left
level: 3
---

# Grafana
Visualização dos dados, faz parte da stack opensource da Grafana Labs
<br>

![grafana](/public/grafana-dashboard.png){width=80%}

---
transition: slide-left
level: 3
---

# Tempo
Backend para rastreamento distribuido, faz parte da stack opensource da Grafana Labs

---
transition: slide-left
level: 3
---

# Mimir
Armazenamento de métricas, faz parte da stack opensource da Grafana Labs

---
transition: slide-left
level: 3
---

# Beyla
Auto instrumentação baseada em eBPF, faz parte da stack opensource da Grafana Labs

---
transition: slide-left
layout: section
level: 1
---

# Prometheus

---
transition: slide-left
hideInToc: true
level: 3
---

# Prometheus
Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud.

---
transition: slide-left
level: 1
---

# Por Onde Começar a Aprender Mais Sobre?
- https://dosedetelemetria.com/
- https://opentelemetry.io/docs/what-is-opentelemetry/
- https://www.oreilly.com/library/view/observability-engineering/9781492076438/

---
layout: center
class: text-center
hideInToc: true
---

## Obrigado pela atenção!
<br>

![](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHl4OGZic3V6NndmY2RiN2UxYmlxbWcxMHZpZGVuY2x4YmxjNnViYiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xUPOqo6E1XvWXwlCyQ/giphy.gif)
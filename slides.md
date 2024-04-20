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

<style>
  img {
  float: right;
  width: 40%;
}
</style>

![Chiquinha - "posso fazer uma observação?"](https://i.makeagif.com/media/4-17-2017/RxTDJa.gif)

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/edsoncelio/observability-101" target="_blank" alt="GitHub" title="Open in GitHub"
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

# Pilares

---
transition: slide-left
hideInToc: true
level: 3
---

# Logs

Um log é um registro de texto com marcação de data/hora, estruturado (recomendado) ou não estruturado, com metadados. De todos os sinais de telemetria, os logs são os que têm o maior legado. A maioria das linguagens de programação possui bibliotecas de logging de forma nativa.

<br>

```bash
I, [2021-02-23T13:26:23.505892 #22473]  INFO -- : [6459ffe1-ea53-4044-aaa3-bf902868f730] Started GET "/" for ::1 at 2021-02-23 13:26:23 -0800
```

---
transition: slide-left
level: 3
---

# Métricas

Uma métrica é uma medida de um serviço capturado em tempo de execução. O momento de captura de uma medida é conhecido como evento métrico, que consiste não apenas na medida em si, mas também no momento em que ela foi capturada e nos metadados associados.

<br>

```bash
avg(rate(node_cpu{job="default/node-exporter",mode="idle"}[1m]))
```
---
transition: slide-left
level: 3
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
  ....

```

---
transition: slide-left
layout: section
level: 1
---


# Ferramentas e Frameworks

---
transition: slide-left
layout: section
level: 2
---


# Projeto OpenTelemetry (OTEL)

<style>
  img {
  display: block;
  margin: auto;

}
</style>

![otel logo](/public/otel-logo.png){width=34%}

---
transition: slide-left
level: 2
---

O OpenTelemetry é um **framework de Observabilidade** projetado para **criar e gerenciar dados de telemetria**, como rastros, métricas e logs. Por design, o OpenTelemetry é **agnóstico a fornecedor e ferramenta**, o que significa que pode ser usado com grande variedade de backends de Observabilidade.

O OpenTelemetry satisfaz a necessidade de observabilidade ao mesmo tempo que segue dois princípios fundamentais:

- Você possui os dados que você gera. Não há dependência de fornecedor (o famoso vendor lock-in).
- Você só precisa aprender um único conjunto de APIs e convenções.

<br>
<br>
<br>

<footer>

[https://opentelemetry.io/](https://opentelemetry.io/docs/)

</footer>

---
transition: slide-left
level: 3
---

## Arquitetura

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![otel](/public/otel.png){width=75%}

---
transition: slide-left
hideInToc: true
level: 3
---

## Componentes

<br>

- Especificação para todos os componentes
- Collector
- Implementações de API e SDK específicas para cada linguagem
- Outras ferramentas, como Operator do Kubernetes, Helm Charts e outros recursos para FaaS

---
transition: slide-left
layout: section
level: 2
---

# Stack da Grafana Labs

<style>
  img {
    display: block;
    margin: auto;
  }
</style>

![grafana grot](/public/grafana-grot.svg){width=20%}

---
transition: slide-left
hideInToc: true
level: 3
---

# Loki
O Loki é um agregador de logs com alta disponibilidade, multi-tenant e escalável inspirado no Prometheus.
Foi projetado para ser econômico e fácil de manter.

Diferente de outras ferramentas, o Loki indexa apenas os metadados dos logs (labels).


<style>
  img {
  display: block;
  margin: auto;
}
</style>

![loki](/public/loki.png){width=76%}

<br>
<footer>

[https://grafana.com/docs/loki/](https://grafana.com/docs/loki/latest/)

</footer>


---
transition: slide-left
level: 3
---

# Grafana
Visualização dos dados, faz parte da stack opensource da Grafana Labs

<br>

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![grafana](/public/grafana-dashboard.png){width=76%}

[https://grafana.com/docs/grafana/](https://grafana.com/docs/grafana/latest/)


---
transition: slide-left
level: 3
---

# Tempo
Backend para rastreamento distribuido, faz parte da stack opensource da Grafana Labs

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![tempo](/public/tempo.png){width=76%}

<br>

<footer>

[https://grafana.com/docs/tempo/](https://grafana.com/docs/tempo/latest/)

</footer>

---
transition: slide-left
level: 3
---

# Mimir
Armazenamento de métricas, faz parte da stack opensource da Grafana Labs.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![tempo](/public/mimir.svg){width=76%}

<br>

<footer>

[https://grafana.com/docs/mimir/](https://grafana.com/docs/mimir/latest/)

</footer>

---
transition: slide-left
level: 3
---

# Beyla
Auto instrumentação baseada em eBPF, faz parte da stack opensource da Grafana Labs


<style>
  img {
  display: block;
  margin: auto;
}
</style>

![beyla](/public/beyla.png){width=74%}

<footer>

[https://grafana.com/docs/beyla/](https://grafana.com/docs/beyla/latest/)

</footer>

---
transition: slide-left
layout: section
level: 2
---

# Prometheus

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![prometheus](/public/prometheus.png){width=8%}

---
transition: slide-left
hideInToc: true
level: 3
---

# Prometheus
O Prometheus é um conjunto de ferramentas de monitoramento e alerta de código aberto que cresceu em popularidade junto com o crescimento do Kubernetes.


<footer>

[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)

</footer>


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

[edsoncelio.dev/observability-101](https://edsoncelio.dev/observability-101)

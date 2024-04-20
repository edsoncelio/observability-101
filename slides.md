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
layout: section
level: 1
---

# O Problema

<style>
  img {
  display: block;
  float: right;

}
</style>

<br>
<br>

![crazy](/public/crazy.gif){width=30%}


---
transition: slide-left
layout: quote
level: 1
hideInToc: true
---

- Muitos serviços se comunicando em diferentes linguagens com diferentes arquiteturas
- Falta de visibilidade do que está acontecendo
- Trabalho de detetive para identificar problemas
- Ações reativas mais que proativas

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

Observabilidade é a capacidade de medir os estados internos de um sistema examinando suas saídas.

A observabilidade nos permite compreender um sistema a partir do exterior, permitindo fazer perguntas sobre esse sistema sem conhecer o seu funcionamento interno. Além disso, permite solucionar facilmente e lidar com novos problemas e ajuda a responder à pergunta: “Por que isso está acontecendo?

---
transition: slide-left
layout: section
level: 1
---

# Dados de Telemetria Importantes de Conhecer

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

Métricas são uma representação numérica de dados medidos em intervalos de tempo.

As métricas economizam tempo porque podem ser facilmente correlacionadas entre os componentes da aplicação/infraestrutura para fornecer uma visão abrangente da integridade e do desempenho do sistema. Também permitem uma pesquisa mais fácil e uma retenção estendida de dados.

<br>

```bash
avg(rate(node_cpu{job="default/node-exporter",mode="idle"}[1m]))
```

Outros exemplos:

- Taxa de erros
- Uso de CPU


---
transition: slide-left
level: 3
---

# Rastros (Traces)
Os rastros nos dão uma visão geral do que acontece quando é feita uma requisição em uma aplicação.
Independente da arquitetura da sua aplicação, os rastros são essenciais para entender o caminho completo
das requisições na aplicação.

## Spans 
Um Span representa uma unidade de trabalho (ou operação).   
Spans são os blocos que compõem os rastros.

<style>
  img {
  display: block;
  margin: auto;

}
</style>

![otel logo](/public/trace.png){width=39%}


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

# OpenTelemetry (OTEL)

<style>
  img {
  display: block;
  margin: auto;

}
</style>

![otel logo](/public/otel-logo.png){width=22%}

---
transition: slide-left
level: 2
---

O OpenTelemetry, também conhecido como Otel é um **framework de Observabilidade** projetado para **criar e gerenciar dados de telemetria**, como rastros, métricas e logs. Por design, o OpenTelemetry é **agnóstico a fornecedor e ferramenta**, o que significa que pode ser usado com grande variedade de backends de Observabilidade.

O OpenTelemetry atende a necessidade de observabilidade ao mesmo tempo que segue dois princípios fundamentais:

- Os dados que você gera são seus. Não há dependência de fornecedor (o famoso vendor lock-in).
- Você **só** precisa aprender um único conjunto de APIs e convenções.

<br>

Atualmente, o Otel tem compatibilidade com [mais de 40 fornecedores](https://opentelemetry.io/ecosystem/vendors/) de plataformas de Observabilidade
integrado com muitas bibliotecas e serviços e com um grande número de usuários.

<br>
<br>

<footer>

[https://opentelemetry.io/](https://opentelemetry.io/docs/)

</footer>

---
transition: slide-left
hideInToc: true
level: 3
---

## Componentes

<br>

- Especificação para todos os componentes (API, SDK e Dados)
- Collector (receber, processar e exportar dados de telemetria)
- Implementações de API e SDK específicas para cada linguagem (.NET, Java, Javascript, PHP, Python...)

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

Grafana é uma ferramenta de visualização que permite que você faça consultas, visualize, crie alertas e explore suas métricas, rastros e logs 
onde quer que estejam armazenados.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![grafana](/public/grafana-dashboard.png){width=65%}

[https://grafana.com/docs/grafana/](https://grafana.com/docs/grafana/latest/)


---
transition: slide-left
level: 3
---

# Tempo
Backend para rastreamento distribuído, otimizado para custos e tem como pre-requisito apenas um armazenamento de objetos para funcionar.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![tempo](/public/tempo.png){width=76%}

<footer>

[https://grafana.com/docs/tempo/](https://grafana.com/docs/tempo/latest/)

</footer>

---
transition: slide-left
level: 3
---

# Mimir
Solução para armazenamento escalável e de longo prazo para métricas.

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
Ferramenta para auto instrumentação baseada em eBPF, com suporte para muitas linguagens, como Go, C/C++, Rust, Python, Ruby, Java.
Todos os dados capturados são feitos sem nenhuma alteração no código da aplicação ou outra configuração.

<style>
  img {
  display: block;
  margin: auto;
}
</style>

![beyla](/public/beyla.png){width=64%}

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

<br>

O Prometheus é um conjunto de ferramentas de monitoramento e alerta de código aberto que cresceu em popularidade junto com o crescimento do Kubernetes.

<br>

Funcionalidades:

- Modelo de dados multi dimensional com dados de série temporal (time serie) identificados pelo nome da métrica e pares de chave/valor
- Uma linguagem para consulta das métricas: PromQL
- A coleta dos dados acontece por meio de um modelo pull via HTTP (para coleta via push é feito via um Gateway intermediário)

<br>
<br>

<footer>

[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)

</footer>

---
transition: slide-left
hideInToc: true
level: 3
---

# Componentes

Componentes (sendo que alguns são opcionais):

- Servidor Principal, responsável por fazer scrape e armazenar os dados time series
- Bibliotecas clientes, para instrumentar as aplicações
- Push Gateway, para jobs efêmeros (e batchs) expor métricas
- Exporters, para ajudar a exportar métricas de serviços terceiros para o Prometheus
- Alert Manager, para gerenciamento de alertas a partir do Prometheus

<br>
<br>

<footer>

[https://prometheus.io/docs/introduction/overview/](https://prometheus.io/docs/introduction/overview/)

</footer>

---
transition: slide-left
hideInToc: true
level: 3
---

<br>
<br>
<br>



Para mais ferramentas, recomendo dar uma olhada no landscape da CNCF [aqui](https://landscape.cncf.io/?group=projects-and-products&view-mode=grid&tag=observability)!

---
transition: slide-left
level: 1
---

# Últimas Considerações

- Observabilidade é diferente de monitoramento
- Além das ferramentas mencionadas existem muitas outras (muitas não sendo opensources)
- Entenda bem suas aplicações e o que precisa de telemetria antes de implementar uma ferramenta (ou stack de ferramenta)
- Observabilidade pode ser cara/custosa
- Observabilidade é uma jornada, vai muito além de logs, rastros e métricas

---
transition: slide-left
level: 1
---

# Por Onde Começar a Aprender Mais Sobre?
- Projeto Dose de Telemetria: https://dosedetelemetria.com/
- Documentações do OpenTelemetry: https://opentelemetry.io/docs/what-is-opentelemetry/
- Livro "Observability Engineering": https://www.oreilly.com/library/view/observability-engineering/9781492076438/
- Livro "Distributed Systems Observability": https://www.oreilly.com/library/view/distributed-systems-observability/9781492033431/
---
layout: center
class: text-center
hideInToc: true
---

## Obrigado pela atenção!
<br>

![](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZHl4OGZic3V6NndmY2RiN2UxYmlxbWcxMHZpZGVuY2x4YmxjNnViYiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xUPOqo6E1XvWXwlCyQ/giphy.gif)

[edsoncelio.dev/observability-101](https://edsoncelio.dev/observability-101)

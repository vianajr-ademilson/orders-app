# Por que não contratar um serviço terceirizado?

Essa é uma pergunta legítima. Existem diversas ferramentas no mercado para gestão de pedidos e vendas. Antes de partir para o desenvolvimento, tentei algumas alternativas.

## Tentativas anteriores

Formulários e ferramentas como Notion foram testados. O problema não era a ferramenta em si, mas o modelo de dados do negócio: **um único pedido pode conter vários produtos**. Em qualquer ferramenta genérica, isso significa preencher múltiplas entradas para registrar um único cliente — um processo repetitivo e propenso a abandono, especialmente em uma operação com vários clientes por dia.

A solução própria resolve isso com uma interface projetada para esse fluxo específico: o usuário lança um pedido inteiro de uma vez, independente de quantos produtos ele contenha, ou pode até inserir o pedido por linguagem natural pelo agente.

## Serviços completos

Sistemas como Omie são soluções robustas com vantagens reais: nota fiscal integrada, gestão financeira, suporte profissional e acesso pelo celular. Vale reconhecer isso.

O problema é que o Omie é um ERP — projetado para gestão financeira e fiscal, não para operação de campo. O problema central aqui era outro: saber exatamente **quantos maços colher por produto** e **quanto entregar por rota**, no dia, de forma rápida. Essa visão operacional específica dificilmente existe de forma simples em um ERP generalista.

## Visão de longo prazo: além dos pedidos

O app de pedidos é a primeira camada de uma plataforma maior. A visão inclui expandir o sistema para automações a nível de hardware — sensores e microcontroladores integrados à própria horta.

Você pode ler mais sobre essas projeções na [seção de projeções do README](README.md#projeções).

## Limitação para o futuro

Esse é talvez o ponto mais importante. O app de pedidos é a **primeira camada de uma plataforma maior**. A visão de longo prazo inclui automações a nível de hardware: sensores e microcontroladores integrados à horta para monitorar e automatizar processos críticos da operação.

Um exemplo concreto: sem energia elétrica, a bomba d'água para de operar e a hidroponia fica sem circulação de água — o que pode comprometer toda a produção. Um sistema de alertas integrado resolve isso em tempo real.

Contratar uma solução terceirizada para gestão de pedidos significaria chegar nessa fase com uma infraestrutura que não suporta integração com hardware, obrigando a manter dois sistemas separados e sem comunicação entre si.

Com infraestrutura própria (backend + banco de dados + servidor), os dados de sensores e microcontroladores podem ser recebidos, armazenados e utilizados na mesma plataforma — de forma integrada com os dados comerciais já existentes.

## Resumo

| Critério | Solução terceirizada | Solução própria |
|---|---|---|
| UX para o fluxo de pedidos | Genérica, muitas entradas | Projetada para o caso específico |
| Custo | Recorrente | Infraestrutura própria |
| Integração com hardware futuro | Inviável | Nativa |
| Controle sobre os dados | Limitado | Total |

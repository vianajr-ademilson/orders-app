# Visão geral

## Problemas que inspiraram o início do projeto

Minha família tem uma hidroponia, e muitos dos processos deles eram feitos pelo WhatsApp, que apeasar de funcional havia algumas complicações operacionais do dia a dia.

- No momento da colheita eles tinha que somar todos os pedidos, o que havia muita margem para erro humano, ainda mais considerando a correria do dia a dia. Ocasionalmente resultando em maços colhidos a mais (disperdicio e prejuíso) ou a menos (problema nas entregas).
- No momento de distribuir para a entrega, reforça novamento os problema descritos previamente, em que tinham que calcular a distribuição das rotas manualmente.
- Falta de base de dados para análise: Apesar deles terem todo o hitórico de pedidos no WhatsApp, não havia como garantir a persistencia dos dados nem utilizá-los para análises.

Principalmente diante desse problemas eu vim procurando alternativas para ajudar, muitas das tentativas falharam até que essa finalmente funcionou.

## Princiapais funcionalidades do App

(Primeiro vou descrever de forma funcional para depois descrever de forma técnica)

- **Lançamento de pedidos de forma simples e rápida**: Uma resistência que as pessoas têm é de preencher formulários (já que 1 pedido pode ter vários produtos) então nessa aplicação o processo de lançamento de pedidos é simplificado. Ao invés de preencher vários formulários para um pedido, o usuário lança apenas um pedido (que internamente se decompõe pela modelagem de dados)
- **Alterar e deletar pedidos**
- **Resumo diário**
    - Quantidade total de produtos: Auxilia no momento da colheita
    - Quantidade total de produtos por rota: Auxilia no monto de distribuir para a entrega
- **Histórico de vendas persistente**: Os pedidos são armazenados em Banco de dados
- **Dashboard**: Com base no banco de dados podemos criar análises como melhor e priores produtos ou clientes, identificar sazonalidade, utiliza como fonte de dados para machine learning entre outras outras análises.

## Funcionalidades adicionais

- **Agente de IA**: Um agente capaz de responder perguntas sobre os pedidos ou até inserir pedidos em lote, simplificando ainda mais o processo de lançamento de pedidos entre outras finalidades.

# Detalhes técnicos

## Tecnologias utilizadas

- **Backend**: Python + Flask
- **Frontend**: HTML + JavaScript + Tailwind CSS
- **Database**: PostgreSQL
- **Infraestrutura**: VPS
- **CI/CD**: GitHub Actions
- **Automação e agente de IA**: n8n
- **LLM**: Gemini
- **Autenticação**: Google OAuth2

## Banco de dados

- Banco de dados SQL postigres, hospedado localmente no servidor
- Não entrarei em muitos detalhes sobre o schema para não comprometer a segurança, porém há uma boa modelagem de dados relacional para otimização e consistência da operação.

## CI/CD

- Pipeline automatizado de build e deploy, cobrindo tanto o ambiente de desenvolvimento quanto o de produção.

## Agent

- **MCP**: Antes de criar o próprio agente, eu criei um MCP server que expõe as funcionalidades da aplicação de forma estruturada para ser consumido pelo agente de IA.
- **Agente**: Criei uma UI que envia webhooks para um agente (criado no n8n) como mensagem. podendo utilizar o MCP para responder os prompts. Utilizei uma simples memória em Window Buffer Memory, que apesar de não salvar um histórico de conversa, consegue manter o contexto das mensagens das sessões ativas.

## Camada de segurança

- **Autenticação**: SSO com Google OAuth2 + controle de acesso por roles (admin/user)
- **Proteção da aplicação**: Medidas contra os ataques mais comuns (injeção, XSS, CSRF, força bruta)
- **Proteção de rede**: A aplicação fica exposta apenas via túnel CDN, com múltiplas camadas de proteção contra bots, DDoS e tráfego malicioso
- **Banco de dados isolado**: O banco de dados roda em localhost, sem exposição à internet — o acesso é exclusivamente interno à aplicação

## Desempenho

O app é acessado principalmente pelo celular, então o desempenho de carregamento foi uma prioridade. Algumas medidas aplicadas:

- **Banco de dados em localhost**: Elimina a latência de rede na comunicação com o banco, o que gerou uma melhoria significativa nos tempos de resposta
- **Carregamento em duas fases**: Os dados são carregados em paralelo, priorizando o que é necessário para o app ficar interativo primeiro. Os pedidos (que envolvem queries mais pesadas) carregam de forma independente, sem bloquear a interface
- **Cache de assets**: JS, CSS e imagens são servidos com cache de 7 dias. A invalidação é automática a cada deploy via fingerprint baseado no commit SHA
- **CSS estático**: O Tailwind é compilado via CLI gerando apenas as classes utilizadas (~16KB), ao invés de ser carregado via CDN (~3MB com processamento em runtime)
- **Imagens otimizadas**: Assets visuais convertidos para WebP, reduzindo significativamente o tamanho dos arquivos

# Projeções

- **Automações a nível de hardware**: Projetos com sensores (Temperatura, humidade, chuva…) e microcontroladores (esp ou arduíno) para coletar dados, interagir com regadores, bombas,
- **Emissão de notas automática**
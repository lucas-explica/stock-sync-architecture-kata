# Kata de Arquitetura: Sincronização de Estoque Multi-Canal

## O Problema

A RetailMax precisa sincronizar estoque entre seus canais de venda em tempo real. Atualmente, cada sistema mantém seu próprio estoque, causando vendas perdidas e clientes frustrados.

## Contexto

### Sistemas Atuais
- 20 lojas físicas com PDVs
- 1 e-commerce (Shopify)
- 1 ERP legado (Java + Oracle)
- 1 centro de distribuição com WMS

### Problemas
- Sincronização apenas 1x por dia (batch noturno)
- Produtos vendidos online quando em falta no CD
- Lojas recusando vendas de produtos disponíveis
- Zero visibilidade do fluxo de dados

## Requisitos

### Funcionais
- Propagar alterações de estoque em até 30 segundos
- 50 mil produtos ativos
- 500 mil movimentações por dia
- Qualquer sistema pode ser fonte de atualização

### Não Funcionais
- Disponibilidade 99.9%
- Latência máxima 500ms para consultas
- Suportar picos de 5x o volume normal
- Recuperação automática de falhas

### Restrições
- Não alterar sistemas legados drasticamente
- Equipe pequena (2 devs + 1 DevOps)
- Prazo: MVP em 2 meses
- Orçamento limitado

## Volumetria
- 50 mil SKUs
- 500 mil movimentações/dia (normal), 2.5 milhões (pico)
- 10 mil consultas/minuto
- 4 sistemas integrados

## Suas Tarefas

### 1. Arquitetura
Desenhe uma solução incluindo:
- Padrão de integração entre sistemas
- Tecnologia de mensageria
- Estratégia de cache
- Mecanismo de fallback

### 2. Modelo de Dados
Defina:
- Estrutura do evento de movimentação
- Campos essenciais para auditoria
- Como lidar com diferentes tipos de movimentação

### 3. Estratégia de Implementação
- 2 fases principais de implementação
- Como migrar sem parar a operação
- Critério de sucesso do MVP

### 4. Trade-offs
Justifique suas principais escolhas técnicas considerando:
- Consistência vs Performance
- Complexidade vs Prazo
- Custo vs Benefício

## Cenários de Teste

Sua solução deve lidar com:
1. Venda simultânea do último item em 2 lojas
2. Sistema de e-commerce offline por 2 horas
3. Pico de Black Friday (5x volume normal)
4. Falha na rede entre ERP e mensageria

## Entregáveis

1. Diagrama de arquitetura
2. Exemplo de payload do evento
3. Plano de implementação (2 fases)
4. Lista de 3 principais trade-offs

## Objetivo

Foque no essencial: uma solução que funcione, seja implementável no prazo e resolva o problema real do negócio.
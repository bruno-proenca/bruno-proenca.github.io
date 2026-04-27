# Industrial Portal Hub 🏭 | Ambev Case Study

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Node-RED](https://img.shields.io/badge/Node--RED-3.0+-red.svg)](https://nodered.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14+-336791.svg)](https://www.postgresql.org/)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.6+-003545.svg)](https://mariadb.org/)

## 📌 Visão Geral

Este projeto é uma solução de **Inteligência de Dados Industriais** desenvolvida para a planta da **Ambev (Vidros Paraná)**. O objetivo principal é atuar na camada de Tecnologia da Informação (IT), consumindo dados industriais já centralizados para criar uma visualização unificada das operações de **Área Quente** e **Área Fria**.

O sistema atua como um hub centralizado, eliminando a necessidade de extrações manuais de banco de dados e facilitando a tomada de decisão estratégica e a rastreabilidade de lotes.

## 🏗️ Arquitetura do Sistema (Decoupled OT/IT)

A arquitetura foi desenhada para garantir segurança e performance, evitando consultas diretas aos CLPs e utilizando bancos de dados como camada intermediária:

1.  **Origem dos Dados:** As variáveis de processo dos CLPs **Siemens** são armazenadas continuamente nos bancos de dados da planta.
2.  **Integração & Orquestração (Middleware):** O **Node-RED** atua como motor de integração, realizando as consultas (queries) seguras nos bancos de dados, orquestrando fluxos e servindo os dados para a aplicação.
3.  **Processamento de Dados:** Scripts em **Python** e lógicas em SQL são utilizados para tratamento, limpeza e cálculos de performance (KPIs) a partir dos dados brutos.
4.  **Bancos de Dados Consultados:**
    * **MariaDB:** Extração de dados de giro rápido e estados operacionais para os dashboards de tempo real.
    * **PostgreSQL:** Consultas analíticas pesadas, relatórios de longo prazo, histórico de paradas e rastreabilidade de produção.
5.  **Visualização (Frontend):** Dashboards web interativos que consomem os dados tratados, entregando informações claras para operadores e gestores.

## 🚀 Funcionalidades Chave

* **Consumo Eficiente de Dados:** Arquitetura otimizada para não sobrecarregar os bancos de dados industriais.
* **Gestão de Justificativa de Paradas:** Dashboard focado no monitoramento, extração de histórico e classificação de paradas de máquinas NIS.
* **KPIs Dinâmicos:** Cálculo automatizado de eficiência, perdas e produtividade por turno a partir das bases MariaDB/PostgreSQL.
* **Interface Unificada:** Centralização das informações da Área Quente e Fria em uma única plataforma web.

## 🛠️ Tecnologias Utilizadas

* **Linguagens:** Python, JavaScript, SQL.
* **Integração:** Node-RED (APIs e fluxos de dados).
* **Bancos de Dados:** MariaDB, PostgreSQL.
* **Frontend:** HTML5, CSS moderno, bibliotecas de visualização (Chart.js).

## 📈 Impacto Gerado

* Transformação de dados brutos de banco de dados em informações visuais de fácil interpretação.
* Eliminação de planilhas manuais para consolidação de indicadores operacionais.
* Desacoplamento seguro: a equipe de gestão visualiza os dados da fábrica sem necessidade de acesso direto à rede de automação (CLPs).

---

**Desenvolvido por Bruno Proença**
*Técnico de Automação I | Graduando em Engenharia de Software*

[LinkedIn](https://www.linkedin.com/in/bruno-pr0enca/) • [Portfólio Online](https://bruno-proenca.github.io)
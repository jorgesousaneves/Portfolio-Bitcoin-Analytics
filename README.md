# 🪙 Bitcoin Market Analytics | Engenharia de Dados End-to-End

![Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

> **Resumo Executivo:** Pipeline de dados completo (ELT) simulando um ambiente corporativo moderno (Lakehouse). O projeto extrai dados do mercado de criptomoedas, processa via dbt seguindo a arquitetura Medallion e entrega KPIs de volatilidade e tendência para tomada de decisão estratégica.

---

## 🖼️ Visualização do Projeto

![Dashboard Bitcoin](imagens/Dashboard.png)
*(Painel final no Power BI: Monitoramento de Preço, Volatilidade e Tendências)*

---

## 🏗️ Arquitetura da Solução (Medallion)

O pipeline foi desenhado com foco em **governança, qualidade de dados e escalabilidade**.

```mermaid
graph LR
    subgraph "Ingestão (Raw)"
    A[API CoinGecko] -->|Python Script + Pandas| B[(Supabase PostgreSQL\nCamada Bronze)]
    end
    
    subgraph "Transformação (dbt Core)"
    B -->|Limpeza & Deduplicação| C[(Camada Silver\nStaging)]
    C -->|Regras de Negócio & KPIs| D[(Camada Gold\nMarts)]
    end
    
    subgraph "Consumption (Analytics)"
    D -->|Direct Query| E[Power BI Dashboard]
    end
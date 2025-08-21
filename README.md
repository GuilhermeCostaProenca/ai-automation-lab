# ⚡ Youon Intelligence – Plataforma de Inteligência Energética (Exemplo Técnico)

Este repositório apresenta uma arquitetura **completa e escalável** para **ingestão, enriquecimento e análise de dados energéticos** em larga escala.
A proposta é mostrar como dados **públicos** (ANEEL, Receita Federal, IBGE, entre outros) podem ser transformados em **inteligência estratégica** para apoiar decisões técnicas, comerciais e executivas.

⚠️ **Nota importante:** este projeto tem caráter **educacional e exploratório**. Ele não representa um sistema em produção, mas sim um **exemplo prático** de boas práticas em engenharia de software, ciência de dados e arquitetura de sistemas.

---

## 💡 Objetivo

A plataforma demonstra como lidar com **milhões de registros de diferentes fontes**, aplicando técnicas modernas de ETL, modelagem de dados e visualização. Entre as entregas possíveis estão:

* Leads qualificados a partir de dados públicos
* Insights geoespaciais e temporais de consumo e demanda elétrica
* Indicadores de qualidade por município, cliente e distribuidora
* API de consulta e dashboards interativos

O grande diferencial está na **transformação de dados brutos em inteligência acionável**.

---

## 📌 Principais Funcionalidades

* 🔄 **Importação automatizada** de datasets (UCAT, UCMT, UCBT – GDB ou CSV)
* 🧹 **Normalização e transformação** para modelo relacional escalável
* 🧠 **Enriquecimento inteligente** via APIs externas (CNPJá, Google Maps, IBGE)
* 📊 **Visualização avançada** com mapas, séries temporais e agregações
* 🔍 **Pipeline auditável** com versionamento, rastreabilidade e controle de status
* ⚡ **Otimizações de banco** com índices, views e materialized views

---

## 🛠️ Stack Tecnológica

| Camada         | Tecnologias principais                 |
| -------------- | -------------------------------------- |
| Backend        | Python 3.11, FastAPI                   |
| Frontend       | Next.js (React), Tailwind CSS          |
| Banco de Dados | PostgreSQL (Azure) + extensões GIS     |
| ETL / Jobs     | Pandas, GeoPandas, psycopg2, Fiona     |
| Orquestração   | Apache Airflow                         |
| IA / ML        | Scikit-learn, HuggingFace Transformers |
| Deploy         | Docker, Docker Compose, Terraform      |

---

## 📂 Estrutura Modular do Projeto

```bash
youon-intelligence/
├── apps/                  # Aplicações
│   ├── api/               # Backend FastAPI
│   └── frontend/          # Frontend Next.js + Tailwind
├── packages/              # Pacotes reutilizáveis
│   ├── jobs/              # ETL (importers, enrichers, transformers)
│   ├── ai/                # Modelos e inferência
│   ├── database/          # Schema, conexões, índices
│   └── orchestrator/      # DAGs do Airflow
├── infra/                 # Infraestrutura (Docker, Terraform, scripts)
├── data/                  # Datasets, logs e artefatos
├── tests/                 # Testes automatizados (Pytest)
├── docs/                  # Documentação, diagramas, glossário
└── ...
```

Essa organização garante **manutenção simples**, **escalabilidade** e **separação clara de responsabilidades**.

---

## 🧱 Modelo de Banco – Schema `intel_lead`

Principais entidades:

* `lead_bruto` – unidade consumidora base com dados técnicos
* `lead_energia_mensal`, `lead_demanda_mensal`, `lead_qualidade_mensal` – séries temporais mensais
* `import_status` – rastreio detalhado das importações
* `lead_enrichment_log` – etapas do enriquecimento
* Tabelas de domínio – classe, modalidade, grupo de tensão, etc.

📍 **Views e Materialized Views**:

* `lead_com_coordenadas` – une unidades consumidoras a pontos notáveis
* `resumo_energia_municipio`, `resumo_leads_distribuidora`, `resumo_leads_ano_camada` – materializadas com `REFRESH`
* `vw_lead_status_enriquecimento`, `vw_import_status_resumido` – usadas pela API/admin

---

## 🧆 Datasets Públicos Utilizados

* [BDGD ANEEL (Geo)](https://dadosabertos-aneel.opendata.arcgis.com/)
* [ANEEL CSV (UCAT, UCMT, UCBT)](https://dadosabertos.aneel.gov.br/)
* Receita Federal (CNPJá API)
* Google Maps API, IBGE, OpenWeather

---

## 🚀 Como Rodar Localmente

1. Clone o repositório:

   ```bash
   git clone https://github.com/seuusuario/youon-intelligence.git
   cd youon-intelligence
   ```

2. Instale dependências:

   ```bash
   pip install -r requirements.txt
   ```

3. Configure o `.env`:

   ```bash
   cp .env.example .env
   ```

4. Suba a API:

   ```bash
   uvicorn apps.api.main:app --reload
   ```

5. Execute um job:

   ```bash
   python packages/jobs/importers/importer_ucat_job.py
   ```

---

## 🧪 Testes e Qualidade

* Testes automatizados com `pytest`
* Cobertura de jobs, API e pipelines de ML
* Métricas de cobertura com `coverage`

---

## 📆 Deploy e Orquestração

* Containers: `docker-compose up --build`
* Orquestração: DAGs do Airflow (`packages/orchestrator/`)
* Infra como código: Terraform (Azure)

---

## 🔮 Roadmap

* Clusterização geográfica de unidades consumidoras
* Sistema de recomendação de soluções energéticas (Arbitragem, GTD, Backup…)
* Automação da análise de qualidade (DIC/FIC) com ML
* Expansão de dashboards interativos e API pública

---

## 👤 Autor

* **Guilherme Costa Proença** – Engenharia de Software e Dados

---

> “O verdadeiro valor dos dados não está em armazená-los, mas em transformá-los em inteligência.”

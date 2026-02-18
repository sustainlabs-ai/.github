<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.svg">
  <img src="assets/logo-light.svg" alt="Sustainlabs AI" width="280">
</picture>

<br/>

**Turning Sustainability Compliance Into Business Value**

AI-powered platform that streamlines ESG reporting, climate risk assessment, and internal controls.
Built for CFOs, Controllers, CSOs, and IR teams.

[![Website](https://img.shields.io/badge/sustainlabs.ai-0A0A0A?style=for-the-badge&logo=googlechrome&logoColor=white)](https://sustainlabs.ai)

</div>

---

## Platform

<table>
  <tr>
    <td align="center" valign="top" width="25%">
      <br/>
      <a href="https://github.com/sustainlabs-ai/log-pose"><strong>🧭 Log Pose</strong></a>
      <br/><br/>
      <em>Compliance Platform</em>
      <br/><br/>
      Web SPA — interactive dashboard for sustainability reporting, materiality assessment, and climate risk visualization.
      <br/><br/>
      <a href="https://github.com/sustainlabs-ai/log-pose">
        <img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black" />
        <img src="https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" />
        <img src="https://img.shields.io/badge/deck.gl-EF4444?style=flat-square" />
      </a>
    </td>
    <td align="center" valign="top" width="25%">
      <br/>
      <a href="https://github.com/sustainlabs-ai/poneglyph"><strong>🗿 Poneglyph</strong></a>
      <br/><br/>
      <em>ETL Framework & API</em>
      <br/><br/>
      Domain-driven data pipeline following medallion architecture (Bronze → Silver → Gold). Serves processed data via REST.
      <br/><br/>
      <a href="https://github.com/sustainlabs-ai/poneglyph">
        <img src="https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white" />
        <img src="https://img.shields.io/badge/Axum-B7410E?style=flat-square" />
        <img src="https://img.shields.io/badge/DataFusion-D22128?style=flat-square&logo=apache&logoColor=white" />
        <img src="https://img.shields.io/badge/Arrow-D22128?style=flat-square&logo=apache&logoColor=white" />
      </a>
    </td>
    <td align="center" valign="top" width="25%">
      <br/>
      <a href="https://github.com/sustainlabs-ai/ohara"><strong>📚 Ohara</strong></a>
      <br/><br/>
      <em>Risk Modeling Sidecar</em>
      <br/><br/>
      Stateless climate risk compute engine. Evidence-backed physical risk models communicating over HTTP via JSON Schema contracts.
      <br/><br/>
      <a href="https://github.com/sustainlabs-ai/ohara">
        <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
        <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
        <img src="https://img.shields.io/badge/xarray-F5A623?style=flat-square" />
      </a>
    </td>
    <td align="center" valign="top" width="25%">
      <br/>
      <a href="https://github.com/sustainlabs-ai/pluton"><strong>⚙️ Pluton</strong></a>
      <br/><br/>
      <em>Infrastructure as Code</em>
      <br/><br/>
      Cloud resource provisioning — S3, CloudFront, ACM, IAM, Route 53. All infrastructure defined in Terraform.
      <br/><br/>
      <a href="https://github.com/sustainlabs-ai/pluton">
        <img src="https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white" />
        <img src="https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white" />
      </a>
    </td>
  </tr>
</table>

## Architecture

```mermaid
flowchart TB
    CDS["🌍 Copernicus CDS"]

    subgraph PONEGLYPH ["🗿 Poneglyph · Rust"]
        direction TB
        JOBS["poneglyph-jobs<br/>Async runner · reqwest"]
        ETL["poneglyph-etl<br/>DataFusion · Arrow"]
        API["poneglyph-api<br/>Axum · REST"]
        JOBS --> ETL
        ETL --> API
    end

    subgraph OHARA ["📚 Ohara · Python"]
        direction TB
        MODELS["Physical Risk Models<br/>FastAPI · xarray"]
    end

    subgraph INFRA ["⚙️ Pluton · Terraform"]
        direction TB
        TF["S3 · CloudFront · IAM<br/>ACM · Route 53"]
    end

    CDS -->|"NetCDF / ZIP"| JOBS
    JOBS <-->|"HTTP · JSON Schema"| MODELS
    ETL -->|"Bronze → Silver → Gold"| S3[("☁️ S3<br/>Parquet")]
    S3 --> API
    API -->|"REST API"| LP["🧭 Log Pose<br/>React · Tailwind · deck.gl"]
    TF -.->|"provisions"| S3
    TF -.->|"provisions"| API
    TF -.->|"provisions"| LP

    SCHEMA["📋 JSON Schema<br/>S3 bucket"]
    SCHEMA -.->|"contract"| MODELS
    SCHEMA -.->|"contract"| ETL
```

## Standards & Frameworks

Our platform supports compliance across major sustainability reporting standards:

| Standard | Scope |
|----------|-------|
| **IFRS S1 / S2** | Global sustainability & climate-related disclosures |
| **ESRS** | EU Corporate Sustainability Reporting Directive |
| **TCFD** | Task Force on Climate-Related Financial Disclosures |
| **SASB** | Industry-specific sustainability accounting |
| **GRI** | Global Reporting Initiative — impact materiality |

## Tech Stack

<div align="center">

![Rust](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Apache Arrow](https://img.shields.io/badge/Apache_Arrow-D22128?style=for-the-badge&logo=apache&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

</div>

---

<div align="center">
  <sub>Sustainlabs AI S.A. de C.V. 2025–2026. All Rights Reserved.</sub>
</div>

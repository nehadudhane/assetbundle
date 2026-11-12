# Databricks Asset Bundles — Jobs and Pipeline Configuration

A Databricks Asset Bundles (DAB) project that organizes a Databricks job, a declarative pipeline, Python notebooks, and supporting project files in one source-controlled repository. The bundle defines **development** and **production** deployment targets.

> This repository showcases the project's existing configuration and sample workloads. The documentation reflects the files currently committed; it is not a deployment verification report.

## Technology Stack

- **Databricks Asset Bundles** for resource configuration and environment targets
- **Databricks Jobs** for notebook-based workflow tasks
- **Databricks declarative pipelines** for a sample table definition
- **Python / PySpark** for notebooks and utility code
- **YAML** for bundle and pipeline resource definitions
- **pytest** for test scaffolding

## Project Components

### 1. Bundle configuration

[`dabproject/databricks.yml`](dabproject/databricks.yml) declares the `dabproject` bundle, variable definitions, and two targets:

- **dev** — development mode, the default target
- **prod** — production mode with an explicitly configured workspace deployment location and permission

The file includes workspace-specific values. Review and adapt those values before using the bundle in another environment.

### 2. Job and notebook

The repository contains:

- [`dabproject/resources/jobs/job.yml.ipynb`](dabproject/resources/jobs/job.yml.ipynb) — an exported Databricks notebook containing an `ingestion_job` YAML definition
- [`dabproject/src/notebooks/ingestion.ipynb`](dabproject/src/notebooks/ingestion.ipynb) — a Python notebook that receives a catalog name through a widget and queries `information_schema.columns` using Spark SQL

The notebook demonstrates parameter-driven metadata inspection. Despite the file name `ingestion`, its checked-in code does **not** ingest external records.

### 3. Declarative pipeline

[`dabproject/resources/pipelines/demopipeline.yml`](dabproject/resources/pipelines/demopipeline.yml) defines a demonstration pipeline with configuration for a catalog, schema, and serverless execution.

Its transformation code is at [`dabproject/src/pipelines/demopipeline/transformations/transformation.py`](dabproject/src/pipelines/demopipeline/transformations/transformation.py). The sample `transformed` table is created from `spark.range(10)`.

### 4. Python utilities and tests

- [`utils.py`](dabproject/src/pipelines/demopipeline/utilities/utils.py) provides a PySpark UDF that checks whether an email address matches a basic regular-expression format.
- [`tests/`](dabproject/tests/) contains sample test scaffolding from the project template.
- [`pyproject.toml`](dabproject/pyproject.toml) includes Python project metadata and development tooling.

The sample taxi test references code not present in this repository. It should not be interpreted as evidence of passing tests.

## Repository Structure

```text
assetbundle/
├── README.md
├── demo.ipynb
└── dabproject/
    ├── README.md
    ├── databricks.yml
    ├── pyproject.toml
    ├── resources/
    │   ├── jobs/
    │   │   └── job.yml.ipynb
    │   ├── pipelines/
    │   │   └── demopipeline.yml
    │   └── variables/
    │       └── environments.yml
    ├── src/
    │   ├── notebooks/
    │   │   └── ingestion.ipynb
    │   └── pipelines/
    │       └── demopipeline/
    │           ├── README.md
    │           ├── transformations/
    │           │   └── transformation.py
    │           └── utilities/
    │               └── utils.py
    ├── tests/
    └── fixtures/
```

Other development-support files, including `.gitignore`, `.vscode/`, `AGENTS.md`, and `CLAUDE.md`, are also included.

## Working with the Bundle

The nested [`dabproject/README.md`](dabproject/README.md) contains the generated project's setup guidance, including Databricks CLI usage.

When using a Databricks Asset Bundle in your own workspace, authenticate using an appropriate account and review environment-specific settings before attempting validation or deployment. This repository does not contain a verified end-to-end execution report.

## Scope

This repository illustrates how Databricks project assets can be organized together with environment-specific configuration, a notebook task, and a sample declarative pipeline. It is a **demonstration project**, not a claim of a production-scale data processing architecture.

## Author

**Neha Dudhane** — [GitHub](https://github.com/nehadudhane)

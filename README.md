# BuildProject-Data-Pipeline

## Purpose
There are multiple environments for a software product: development, testing, sandbox, UAT, staging, and production. When developing new features or debugging in the development environment, you always want to use realistic data to ensure the quality of the work. The production database has the data we are looking for, but it contains confidential information. So we need to automate/orchestrate a batch-processing ETL data pipeline such that it will sanitize or obfuscate the original data before moving forward. Sometimes it's reasonable to minimize the original database since certain environments don't need the full database to produce high-quality work, while optimizing the time, storage, and cost resources.

## ETL Data Pipeline Diagram (Directed Acyclic Graph)
![DAG image](https://github.com/StevenG777/BuildProject-Data-Pipeline/blob/main/Pipeline_dag.jpg)

## Software System Diagram
Crafting diagram in progress ...

## Features
- Dynamic Rule Engine that performs various pipeline operations based on the template
  - Dynamic ETL pipeline creation via YAML configuration
  - Copy data between MongoDB databases
  - Sanitize or obfuscate sensitive fields
  - Minimize data to save computing and storage resources
- Data pipeline orchestration using an industry tool like Apache Airflow
- Batch processing with memory-aware sizing, preventing containers from running out of memory when processing the data all at once

## Tech Stack
- Languages: Python
- Linting: Pylance
- Database: MongoDB & PyMongo
- Synthetic Data Generation: Faker
- Pipeline Orchestrator: Apache Airflow 
- Containerization: Docker & Docker Compose
- Configuration: YAML
- Testing: Unittest

## YAML configuration rules
### Description: 
The YAML config rule acts as the Rule/Template in the Dynamic Rule Engine, which allows granular and flexible control of specific transformations for a particular field, collection, and database level, where the details of granularity are mentioned in the "Format" section. The engine in the Dynamic Rule Engine is the operations in the data pipeline pre-defined by the YAML config rule.

### Format:
- pipeline: Specify that this is a pipeline configuration
  - step: Description of what this particular stage of the data pipeline does
  - type: We provided limited options of a (transformation) module you can choose in literal strings: [copy, sanitize_obfuscate, minimize, (refresh) <-- upcoming option]
  - order: Order in the data pipeline to perform the task
  - source_db: Source database you are extracting the data from
  - dest_db: Destination database you are loading the data to
  - collections: Collection (table) of the database you are targeting
    - fields: Field (column) for each document (row/record) you are targeting
      - strategy: The options of the sanitization/obfuscation function in literal strings: [redact, substitute, perturb, hash_salt, (field_removal, doc_removal) <-- upcoming option] and minimization function in literal strings: [sample, MORE coming in the future]
      - params: set of key-value parameters for feeding into the strategy functions, so it works properly

### Example:
```yaml
pipelines:
  - step: sanitize_clean
    type: sanitize_obfuscate
    order: 2
    source_db: financial_data_clean
    dest_db: financial_data_clean
    collections:
      customers:
        username: {strategy: substitute, params: {field_type: username}}    
```
To see the full config file, please reference this [YAML file](https://github.com/StevenG777/BuildProject-Data-Pipeline/blob/main/configs/pipeline_configs.yml)

## Functionalities:
Writing In Progress ...

## How to run the data pipeline
Writing In Progress ...

## Future Development
- Continue the data pipeline with the data refresh module
- More functions, more Sanitization, Obfuscation, Minimization
- Sanitization/Obfuscation of nested data field, rather than just a flat data field
- Learn how to build a data pipeline that complies with data privacy regulation, governance, and provenance
- Data Validation using Pydantic
- Use Docker Swarm/Kubernetes for container scaling/fault tolerance
- Explore Cloud platform for Docker, MongoDB, and Airflow
- Build a similar pipeline, but for PostgreSQL
- Flatten the MongoDB Production DB and pipeline to the Data Warehouse for Ad-hoc analysis and dashboard

# BuildProject-Data-Pipeline

## Data Pipeline Diagram (Directed Acyclic Graph)
![DAG image](https://github.com/StevenG777/BuildProject-Data-Pipeline/blob/main/Pipeline_dag.jpg)

## Purpose
There are multiple environments for a software product: development, testing, sandbox, UAT, staging, and production. When developing new features or debugging in the development environment, you always want to use realistic data to ensure the quality of the work. The production database has the data we are looking for, but it contains confidential information. So we need to automate/orchestrate a data pipeline such that it will sanitize or obfuscate the original data before moving forward. Sometimes it's reasonable to minimize the original database since certain environments don't need the full database to produce high-quality work, while optimizing the time, storage, and cost resources.

## Tech Stack
- Languages: Python
- Linting: Pylance
- Database: MongoDB & PyMongo
- Synthetic Data Generation: Faker
- Pipeline Orchestrator: Apache Airflow 
- Containerization: Docker & Docker Compose
- Configuration: YAML
- Testing: Unittest

## Future Development
- Continue the data pipeline with the data refresh module
- More functions, more Sanitization, Obfuscation, Minimization
- Sanitization/Obfuscation of nested data field, rather than just a flat data field
- Learn how to build a data pipeline that complies with data privacy regulation, governance, and provenance
- Data Validation using Pydantic
- Use Docker Swarm/Kubernetes for container scaling/fault tolerance
- Explore Cloud platform for Docker, MongoDB, and Airflow
- Build a similar pipeline, but for PostgreSQL
- Flatten MongoDB Production DB and pipeline to Data Warehouse for Ad-hoc analysis and dashboard

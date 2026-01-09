Voici la table des matières complète du livre **"Architecting an Apache Iceberg Lakehouse"** par Alex Merced :[1]

## **PART 1: THE VALUE OF THE APACHE ICEBERG LAKEHOUSE**

### **Chapitre 1 - THE WORLD OF THE APACHE ICEBERG LAKEHOUSE**
- 1.1 What is a data lakehouse
  - 1.1.1 The rise of data warehouses
  - 1.1.2 The move to cloud data warehouses
  - 1.1.3 The data lake and the Hadoop era
  - 1.1.4 Apache Iceberg: The key to the data lakehouse
  - 1.1.5 The data lakehouse: the best of both worlds
- 1.2 What is Apache Iceberg?
  - 1.2.1 The need for a table format
  - 1.2.2 How Apache Iceberg manages metadata
  - 1.2.3 Key features of Apache Iceberg
  - 1.2.4 Apache Iceberg as an open-source standard
- 1.3 The benefits of Apache Iceberg
  - 1.3.1 ACID transactions
  - 1.3.2 Table evolution
  - 1.3.3 Time travel & snapshot-based queries
  - 1.3.4 Hidden partitioning for reduced accidental full-table scans
  - 1.3.5 Cost efficiency & optimized query performance
- 1.4 The components of an Apache Iceberg lakehouse
  - 1.4.1 The storage layer: The foundation of your lakehouse
  - 1.4.2 The ingestion layer: Feeding data into Iceberg tables
  - 1.4.3 The catalog layer: The entry point to your lakehouse
  - 1.4.4 The federation layer: Modeling & accelerating data
  - 1.4.5 The consumption layer: Delivering value to the business
- 1.5 Summary

### **Chapitre 2 - HANDS-ON WITH APACHE ICEBERG**
- 2.1 Setting up an Apache Iceberg environment
  - 2.1.1 Prerequisites: Install Docker
  - 2.1.2 Creating the Docker compose file
  - 2.1.3 Running the environment
  - 2.1.4 Accessing the services
- 2.2 Creating Iceberg tables in Spark
  - 2.2.1 Populating the PostgreSQL database
  - 2.2.2 Starting the Apache Spark environment
  - 2.2.3 Configuring Apache Spark for Iceberg
  - 2.2.4 Loading data from PostgreSQL into Iceberg
  - 2.2.5 Verifying data storage in MinIO
- 2.3 Reading Iceberg tables in Dremio
  - 2.3.1 Starting Dremio
  - 2.3.2 Connecting Dremio to the Nessie Catalog
  - 2.3.3 Querying Iceberg tables in Dremio
- 2.4 Creating a BI dashboard from your Iceberg tables
  - 2.4.1 Starting Apache Superset
  - 2.4.2 Connecting Superset to Dremio
  - 2.4.3 Creating a dataset from Iceberg tables
  - 2.4.4 Building charts and dashboards
- 2.5 Summary

## **PART 2: DESIGNING YOUR ICEBERG ARCHITECTURE**

### **Chapitre 3 - PREPARING FOR YOUR MOVE TO APACHE ICEBERG**
- 3.1 Conducting your data platform audit
  - 3.1.1 Who are the stakeholders?
  - 3.1.2 What should you ask stakeholders?
  - 3.1.3 Conducting a technological audit
- 3.2 Hamerliwa Bank's audit in action
  - 3.2.1 Hamerliwa Bank interviews their stakeholders
  - 3.2.2 Hamerliwa Bank audits its technology
  - 3.2.3 Hamerliwa Bank summarizes its audit findings
- 3.3 From audit to requirements: Laying the foundation for design
  - 3.3.1 Defining storage requirements
  - 3.3.2 Defining ingestion requirements
  - 3.3.3 Defining catalog requirements
  - 3.3.4 Defining federation requirements
  - 3.3.5 Defining consumption requirements
  - 3.3.6 Hamerliwa Bank establishes its requirements
- 3.4 Architectural plan and road show
  - 3.4.1 Hamerliwa Bank creates its architectural plan
  - 3.4.2 Hamerliwa Bank conducts a road show
- 3.5 Summary

### **Chapitre 4 - SELECTING THE STORAGE LAYER**
- 4.1 Storage requirements
  - 4.1.1 File retrieval performance requirements
  - 4.1.2 Security requirements
  - 4.1.3 Integrity requirements
  - 4.1.4 Cost and operational overhead requirements
- 4.2 Block vs object
  - 4.2.1 Block storage
  - 4.2.2 Object storage
- 4.3 The standards in the storage layer
  - 4.3.1 Apache Parquet
  - 4.3.2 The S3 API
- 4.4 Storage solutions
  - 4.4.1 Vendor Comparison Summary
  - 4.4.2 Hadoop (HDFS)
  - 4.4.3 Amazon S3
  - 4.4.4 Google Cloud Storage
  - 4.4.5 Azure Blob Storage and ADLS
  - 4.4.6 MiniO
  - 4.4.7 Ceph
  - 4.4.8 NetApp StorageGRID
  - 4.4.9 Pure Storage
  - 4.4.10 Dell ECS
  - 4.4.11 Wasabi
- 4.5 Selecting based on requirements
  - 4.5.1 Performance requirements
  - 4.5.2 Security requirements
  - 4.5.3 Integrity requirements
  - 4.5.4 Cost and operational requirements
- 4.6 Summary

### **Chapitre 5 - ARCHITECTING THE INGESTION LAYER**
- 5.1 Ingestion requirements
  - 5.1.1 Ingestion throughput and latency
  - 5.1.2 Reliability and fault tolerance
  - 5.1.3 Schema management and evolution
  - 5.1.4 Operational complexity and maintainability
- 5.2 Ingestion models and architectures
  - 5.2.1 Batch ingestion
  - 5.2.2 Micro-batch and incremental ingestion
  - 5.2.3 Streaming ingestion
- 5.3 How Iceberg manages writes
  - 5.3.1 Write semantics in Iceberg
  - 5.3.2 Commit protocols and conflict handling
- 5.4 Tools and frameworks for ingestion
  - 5.4.1 Apache Spark
  - 5.4.2 Apache Flink
  - 5.4.3 Apache NiFi
  - 5.4.4 Fivetran
  - 5.4.5 Qlik
  - 5.4.6 Airbyte
  - 5.4.7 Confluent
  - 5.4.8 Redpanda
  - 5.4.9 Cloud-native ingestion services
  - 5.4.10 Tool selection considerations
- 5.5 Applying ingestion requirements in context
  - 5.5.1 Prioritizing low latency
  - 5.5.2 Managing high throughput
  - 5.5.3 Supporting complex transformations
  - 5.5.4 Handling schema evolution
  - 5.5.5 Balancing operational overhead
  - 5.5.6 Considering existing cloud environments
- 5.6 Summary

### **Chapitre 6 - IMPLEMENTING THE CATALOG LAYER**
- 6.1 The role of the catalog in Apache Iceberg lakehouses
  - 6.1.1 Responsibilities of the catalog
  - 6.1.2 Catalog interactions with query and processing engines
- 6.2 Evaluating catalog requirements
  - 6.2.1 Performance, availability, and scale
  - 6.2.2 Metadata governance and lineage
  - 6.2.3 Security and compliance
  - 6.2.4 Deployment flexibility and ecosystem compatibility
  - 6.2.5 Cost and operational overhead
  - 6.2.6 Catalog federation and mesh architectures
- 6.3 Apache Iceberg REST Catalog Spec
  - 6.3.1 Before the Apache Iceberg REST spec
  - 6.3.2 The solution
- 6.4 Catalog options: Exploring the ecosystem
  - 6.4.1 Hadoop Catalog
  - 6.4.2 Hive Catalog
  - 6.4.3 JDBC Catalog
  - 6.4.4 Apache Polaris
  - 6.4.5 Project Nessie
  - 6.4.6 Apache Gravitino
  - 6.4.7 Lakekeeper
  - 6.4.8 AWS Glue Data Catalog
  - 6.4.9 Dremio Catalog
  - 6.4.10 Snowflake Open Catalog
  - 6.4.11 Databricks Unity Catalog
- 6.5 Choosing the right catalog: Evaluating options through scenarios
  - 6.5.1 Scenario: A mid-sized data team migrating from Hive
  - 6.5.2 Scenario: A rapidly scaling cloud-native startup
  - 6.5.3 Scenario: A multinational enterprise with strict data governance
  - 6.5.4 Scenario: SaaS startup prioritizing operational simplicity
  - 6.5.5 Scenario: A large enterprise with multi-cloud and federated governance needs
  - 6.5.6 Scenario: Financial firm requiring daily environment cloning for stress testing
  - 6.5.7 Scenario: Phased Iceberg migration with query federation across legacy systems
  - 6.5.8 Scenario: Lightweight lakehouse adoption with Hadoop catalog and Python
- 6.6 Summary

### **Chapitre 7 - DESIGNING THE FEDERATION LAYER**
- 7.1 What data federation is and why it matters
  - 7.1.1 Common use cases and challenges driving federation needs
  - 7.1.2 How federation aligns with agility and accessibility
- 7.2 Key requirements for federation
  - 7.2.1 Supporting diverse data sources without duplication
  - 7.2.2 Ensuring consistent semantics and business logic
  - 7.2.3 Providing seamless connectivity for analytics tools
  - 7.2.4 Introducing Dremio and Trino
- 7.3 Dremio
  - 7.3.1 Dremio architecture
  - 7.3.2 Dremio's connector ecosystem and Iceberg-centric focus
  - 7.3.3 Dremio's performance enhancements
- 7.4 Trino
  - 7.4.1 Modular architecture for wide-source support
  - 7.4.2 Flexibility and configurability for complex environments
  - 7.4.3 Community-led evolution and vendor extensions
  - 7.4.4 Semantic layer considerations in Trino
- 7.5 Deployment models
  - 7.5.1 Deployment with Dremio
  - 7.5.2 Deployment with Trino
- 7.6 Federation platform decision scenarios
  - 7.6.1 Fragmented multi-source environment: Trino for connector breadth
  - 7.6.2 Building a native Iceberg lakehouse: Dremio for Iceberg-native features
  - 7.6.3 Empowering business users with UI and governed datasets: Dremio
  - 7.6.4 Lightweight querying of Hudi datasets: Trino via AWS Athena
  - 7.6.5 On-prem Cloudera modernization: Trino replacing Impala for performance
  - 7.6.6 Hybrid cloud Iceberg strategy: Dremio bridging on-prem and ADLS
- 7.7 Federation Alternatives
  - 7.7.1 Virtualization via shortcuts in OneLake
  - 7.7.2 AI-native data virtualization with Spice.ai
  - 7.7.3 Choosing the right fit
- 7.8 Summary

### **Chapitre 8 - UNDERSTANDING THE CONSUMPTION LAYER**
- 8.1 Revisiting the benefits of the lakehouse for consumption
- 8.2 Connecting the lakehouse to the people
- 8.3 Revisiting requirements from our audit
  - 8.3.1 Interpreting requirements for consumption
  - 8.3.2 Requirements for BI tools
  - 8.3.3 Requirements for interactive notebook environments
  - 8.3.4 Requirements for AI and specialized data consumption tools
- 8.4 Open interfaces for seamless consumption
  - 8.4.1 JDBC and ODBC
  - 8.4.2 Arrow Flight
  - 8.4.3 Model Context Protocol (MCP)
- 8.5 Business intelligence tools in the lakehouse
  - 8.5.1 Open source BI tools
  - 8.5.2 Commercial BI tools
- 8.6 Tools for AI and machine learning workloads
- 8.7 Choosing the right consumption tools: Ten illustrated scenarios
  - 8.7.1 Startup with a data science focus
  - 8.7.2 Large financial institution with strict governance
  - 8.7.3 Mid-sized e-commerce platform building embedded analytics
  - 8.7.4 Decentralized media organization enabling self-service analytics
  - 8.7.5 Government agency balancing public transparency and internal control
  - 8.7.6 Healthcare provider with compliance and data locality constraints
  - 8.7.7 Logistics company unifying real-time operations and historical analysis
  - 8.7.8 SaaS company offering customizable data access to clients
  - 8.7.9 Nonprofit organization supporting collaborative research
  - 8.7.10 Manufacturing company enabling predictive maintenance
- 8.8 Summary

## **PART 3: OPERATING YOUR APACHE ICEBERG LAKEHOUSE**

Voici la structure complète des **chapitres 9 et 10** du livre "Architecting an Apache Iceberg Lakehouse" par Alex Merced:[1]

## **Chapitre 9 - MAINTAINING AN ICEBERG LAKEHOUSE**

### 9.1 Problem: Suboptimal data files
- 9.1.1 Small files
- 9.1.2 Poorly colocated data
- 9.1.3 Metadata sprawl
- 9.1.4 Merge-on-read (MOR) performance hits

### 9.2 Solution: Compaction
- 9.2.1 What is compaction?
- 9.2.2 Target file size
- 9.2.3 Files to be included
- 9.2.4 Using filters to scope compaction

### 9.3 Storage footprint management and data retention
- 9.3.1 Running snapshot expiration
- 9.3.2 COW vs MOR: Implications for data retention
- 9.3.3 Regulatory considerations for data deletion

### 9.4 Exploring Apache Iceberg's metadata tables

### 9.5 Access controls in an Iceberg lakehouse
- 9.5.1 Storage layer controls
- 9.5.2 Catalog-level controls
- 9.5.3 Engine-level access controls

### 9.6 Summary

***

## **Chapitre 10 - OPERATIONALIZING APACHE ICEBERG**

### 10.1 Orchestrating the lakehouse
- 10.1.1 Choosing orchestration tools and patterns
- 10.1.2 Metadata-driven triggers for proactive maintenance
- 10.1.3 Per-table maintenance policies
- 10.1.4 Monitoring and alerting integration
- 10.1.5 Putting orchestration into practice

### 10.2 Auditing the lakehouse
- 10.2.1 Leveraging snapshot history for change tracking
- 10.2.2 Using branching and tagging for governance
- 10.2.3 Implementing file and snapshot retention policies
- 10.2.4 Practical retention policy orchestration
- 10.2.5 Secure data deletion
- 10.2.6 Access auditing and governance
- 10.2.7 Practical auditing with Iceberg: Example workflows

### 10.3 Disaster recovery in the lakehouse
- 10.3.1 The role of the metadata catalog in disaster recovery
- 10.3.2 Protecting against data loss and corruption
- 10.3.3 Cross-region and multi-environment recovery
- 10.3.4 Rollback and time travel in incident response
- 10.3.5 Automating disaster recovery procedures
- 10.3.6 Validating recovery readiness
- 10.3.7 Disaster recovery through automation
- 10.3.8 Practical examples: Automating recovery workflows

### 10.4 Summary

Voici les **appendices A, B et C au complet** du livre "Architecting an Apache Iceberg Lakehouse" par Alex Merced:[1]

***

## **APPENDIX A: THE METADATA TABLES**

### A.1 Querying Iceberg metadata tables

### A.2 The history metadata table

### A.3 The snapshots metadata table

### A.4 The metadata_log_entries metadata table

### A.5 The manifests metadata table

### A.6 The partitions metadata table

### A.7 The files metadata table

### A.8 The manifests metadata table

### A.9 The partitions metadata table

### A.10 The position_deletes metadata table

### A.11 The all_data_files metadata table

### A.12 The all_delete_files metadata table

### A.13 The all_entries metadata table

### A.14 The all_manifests metadata table

### A.15 The refs metadata table

### A.16 Monitoring table health with metadata tables

***

## **APPENDIX B: PYTHON FOR APACHE ICEBERG**

### B.1 PyIceberg

### B.2 Polars

### B.3 DuckDB

### B.4 Daft

### B.5 Dremio

### B.6 Bauplan

### B.7 SpiceAI

### B.8 Summary and best practices

***

## **APPENDIX C: THE APACHE ICEBERG SPECIFICATION**

### C.1 Understanding the Iceberg specification
- C.1.1 What is a table format specification?
- C.1.2 Why Iceberg formalizes table behavior
- C.1.3 Evolution of the spec: versioning principles and compatibility

### C.2 Iceberg table format versions
- C.2.1 Version 1: Foundation for analytical tables
- C.2.2 Version 2: Row-level deletes and stricter writes
- C.2.3 Version 3: Extended types and advanced capabilities
- C.2.4 Version 4: Performance, portability, and real-time readiness

### C.3 Snapshot management and table metadata
- C.3.1 Table metadata files
- C.3.2 Snapshots and the manifest list
- C.3.3 Sequence numbers and optimistic concurrency

### C.4 The REST Catalog specification
- C.4.1 Overview and purpose
- C.4.2 Catalog configuration and default endpoints
- C.4.3 Namespaces, tables, and views
- C.4.4 Table registration, metrics, and transactions
- C.4.5 OAuth2 support and security considerations
- C.4.6 The scan planning endpoint

### C.5 Puffin file format specification
- C.5.1 What is a Puffin file?
- C.5.2 Storing column-level metrics and custom indexes
- C.5.3 Integration with Iceberg table metadata

### C.6 Compatibility and migration
- C.6.1 Reading and writing across format versions
- C.6.2 Upgrading tables to newer spec versions
- C.6.3 Handling backward compatibility in practice

# AWS Database Migration Service: SQL Server to Amazon Redshift

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Amazon RDS](https://img.shields.io/badge/Amazon%20RDS-527FFF?style=for-the-badge&logo=amazon-rds&logoColor=white)
![Amazon Redshift](https://img.shields.io/badge/Amazon%20Redshift-8C4FFF?style=for-the-badge&logo=amazon-redshift&logoColor=white)
![AWS DMS](https://img.shields.io/badge/AWS%20DMS-FF4F8B?style=for-the-badge&logo=amazon-aws&logoColor=white)
![Microsoft SQL Server](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)
![CloudShell](https://img.shields.io/badge/AWS%20CloudShell-232F3E?style=for-the-badge&logo=gnubash&logoColor=white)

## Project Overview

This project demonstrates an end-to-end database migration solution using AWS Database Migration Service (DMS) to transfer data from a transactional Microsoft SQL Server database on Amazon RDS to Amazon Redshift for analytics and data warehousing workloads. The implementation showcases cloud-native migration patterns, infrastructure configuration, and validation techniques essential for modern data engineering pipelines.

## Lab Objective

Design and implement a fully functional data migration pipeline that seamlessly transfers relational database tables from SQL Server to Amazon Redshift using AWS DMS, while ensuring data integrity, minimal downtime, and adherence to AWS best practices for security and networking configuration.

### Technology Stack

- **Source Database**: Amazon RDS for SQL Server (UniversityDB with UniversityScores table)
- **Target Data Warehouse**: Amazon Redshift (lab-cluster, dev database)
- **Migration Service**: AWS Database Migration Service (DMS 3.5.3)
- **Compute**: DMS Replication Instance (dms.t3.small)
- **Management Tools**: AWS CloudShell, Redshift Query Editor
- **Security**: VPC Security Groups, IAM Roles (myRedshiftRole, DMS service roles)
- **Storage**: Amazon S3 (script hosting and intermediate storage)

## Real-World Business Use Case

### Scenario: University Analytics Platform Migration

A large educational institution maintains operational data in a SQL Server database hosted on Amazon RDS, tracking university rankings, performance metrics, and institutional data across 500+ records. The analytics team requires this data in Amazon Redshift to:

- Perform complex analytical queries on multi-year ranking trends
- Integrate with BI tools (Tableau, QuickSight) for executive dashboards
- Enable data science teams to build predictive models for institutional performance
- Separate OLTP (transactional) workloads from OLAP (analytical) workloads for optimal performance
- Reduce query response times from minutes to seconds for large-scale aggregations

This migration pattern is applicable across industries: retail (sales data warehousing), healthcare (patient analytics), finance (transaction analysis), and SaaS (customer behavior analytics).

## Actions Performed

### Infrastructure & Networking Configuration

- Configured VPC networking with appropriate subnet groups for DMS and Redshift services
- Created and configured security groups with inbound rules for database access (TCP 1433 for SQL Server, TCP 5439 for Redshift)
- Established DMS replication subnet group spanning multiple availability zones for high availability
- Configured publicly accessible endpoints for lab environment testing and validation

### Source Database Preparation

- Provisioned Amazon RDS SQL Server instance with appropriate compute and storage specifications
- Utilized AWS CloudShell to install SQL Server command-line tools (sqlcmd, ODBC drivers)
- Downloaded university ranking dataset from Amazon S3 and loaded 500+ records into UniversityDB
- Created UniversityScores table with appropriate schema and data types
- Validated source data integrity and connection parameters before migration

### AWS DMS Configuration & Migration

- Provisioned DMS replication instance (dms.t3.small) with engine version 3.5.3
- Created and tested source endpoint connection to RDS SQL Server with admin credentials
- Created and tested target endpoint connection to Amazon Redshift cluster
- Configured IAM roles with appropriate policies (AmazonDMSRedshiftS3Role, AmazonDMSVPCManagementRole)
- Designed table mapping rules using schema pattern matching to include all tables in dbo schema
- Executed full-load migration task transferring UniversityScores table from SQL Server to Redshift
- Monitored migration task progress and validated successful completion status

### Target Data Warehouse Setup

- Deployed Amazon Redshift cluster (lab-cluster) with appropriate node type and configuration
- Associated IAM roles (myRedshiftRole with S3ReadOnlyAccess) to enable data loading capabilities
- Configured Redshift security group rules to allow Query Editor and external tool connectivity
- Created dev database with awsuser admin credentials following least-privilege principles

### Validation & Testing

- Executed SQL queries in Redshift Query Editor to validate data migration completeness
- Performed row count comparisons between source (SQL Server) and target (Redshift) tables

## Key Technical Skills Demonstrated

- **Cloud Platforms**: Amazon Web Services (AWS)
- **Database Technologies**: Microsoft SQL Server, Amazon RDS, Amazon Redshift
- **Migration Tools**: AWS Database Migration Service (DMS)
- **Infrastructure as Code**: VPC networking, security groups, subnet groups, IAM policies
- **DevOps Tools**: AWS CloudShell, sqlcmd, ODBC drivers
- **Cloud Security**: IAM roles, security group rules, credential management

## Project Outcomes

1. Successfully migrated relational database from operational SQL Server to analytical Redshift platform
2. Maintained 100% data integrity with zero row loss during migration
3. Established repeatable migration pattern applicable to production-scale implementations
4. Validated cloud-native architecture supporting separation of OLTP and OLAP workloads
5. Gained hands-on experience with enterprise-grade AWS data migration services

## Lessons Learned

- Proper endpoint connectivity testing before task creation prevents migration failures
- Security group configuration is critical for DMS replication instance communication
- IAM role associations must be completed before Redshift can access S3 resources
- Redshift columnar storage provides significant performance benefits for analytical queries
- Table mapping rules offer flexibility for schema-level and pattern-based migrations
- CloudShell provides efficient environment for database administration without EC2 instances


---


*This project is for educational and portfolio demonstration purposes.*


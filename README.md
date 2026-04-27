# Microsoft 365 Third-Party Applications Dataset

This repository contains a curated dataset of Microsoft 365 (M365) third-party applications, including their descriptions and requested OAuth permissions. The dataset supports research on security, privacy, and permission analysis in enterprise application ecosystems.

## Overview

Microsoft 365 applications can request fine-grained OAuth permissions to access organisational resources such as emails, files, calendars, chats, and directories. Permission transparency and consistency vary across distribution channels, making systematic analysis difficult.

This dataset provides a consolidated view of M365 applications by combining metadata from multiple sources. It enables:

- Analysis of permission usage patterns  
- Detection of over-privileged applications  
- Study of alignment between app functionality and requested permissions  

The dataset originates from a larger crawl of over 8,000 applications, of which 1,069 include both descriptions and permission data.

## Dataset Contents

The dataset is provided as a CSV file: `apps_cleaned.csv`

Each row corresponds to a single application.

### Core Fields

The dataset includes the following key attributes:

- App Name / ID  
  Unique identifier or name of the application

- Description  
  Cleaned textual description of the app’s functionality (English only, minimum 10 words)

- Permissions  
  List of OAuth permissions requested by the application

- Optional fields (depending on version)  
  - Source (Marketplace, Teams, SharePoint, University tenant)  
  - Additional metadata (e.g., category, ratings)

## Preprocessing

The dataset has undergone the following processing steps:

- Removal of duplicate applications across sources  
- Resolution of naming inconsistencies (service principals vs marketplace names)  
- Filtering:
  - Non-English descriptions  
  - Descriptions shorter than 10 words  
- Manual validation of ambiguous matches  

Final dataset characteristics:

- 1,069 applications  
- More than 300 distinct permissions  
- Between 1 and 32 permissions per application  

## Data Collection Methodology

Data was aggregated from three main sources:

1. Public APIs  
   - Microsoft Teams app catalogue  
   - SharePoint store  

2. Marketplace Crawling  
   - Automated deployment of applications in a test tenant  
   - Extraction of permissions via Microsoft Entra ID  

3. Operational Tenant Data  
   - Applications from a university M365 tenant (~35,000 users)

Due to the lack of a global application identifier, records were matched using a combination of exact and partial name matching, followed by manual verification.

## Research Context

This dataset was created as part of an ongoing research effort studying the Microsoft 365 application ecosystem from a security and privacy perspective.

The analysis associated with this dataset includes:

- Topic modelling (BERTopic) to cluster applications into functional groups  
- Permission profiling within semantically similar applications  
- Topic-aware anomaly detection using:
  - One-Class SVM  
  - Local Outlier Factor  
  - Isolation Forest  

### Key Observations

- Approximately 13% of applications exhibit anomalous permission patterns  
- Many applications request broad tenant-wide permissions  
- Permission disclosure is inconsistent across distribution channels  
- There are observable mismatches between declared functionality and requested access  

## Important Notes

- No ground truth labels for malicious behaviour are included  
- Anomalies indicate deviation, not necessarily malicious intent  
- Permissions reflect declared or observed scopes, not runtime behaviour  

## Ethical Considerations

- Data was collected from public APIs or anonymised sources  
- No personally identifiable user data is included  
- Tenant-derived data was anonymised prior to analysis  

## Potential Use Cases

This dataset can support:

- Security analysis of enterprise SaaS ecosystems  
- Detection of over-privileged applications  
- Natural language processing tasks (e.g., topic modelling, semantic alignment)  
- Risk scoring and permission auditing tools  
- Research on OAuth ecosystems and access control  

## Limitations

- Only a subset of applications expose both descriptions and permissions  
- Permission visibility depends on installation context  
- Matching across sources may introduce minor inaccuracies  
- Dataset reflects a snapshot in time (2025 crawl)  

## Future Work

Potential extensions include:

- Adding dynamic behaviour analysis  
- Expanding coverage of third-party integrations  
- Improving permission-description alignment models  
- Incorporating real-world risk signals  
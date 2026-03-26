---
title: 'SWAT4HCLS 2026 Biohackathon report: From DCAT to HealthDCAT-AP - Comparative Analysis of National Healthcare Metadata Catalog Schemas to Enable Federated Interoperability in Europe'
title_short: 'SWAT4HCLS 2026 Biohackathon report: From DCAT to HealthDCAT-AP - A Comparative Analysis'
tags:
  - data catalog
  - metadata schema
  - dcat
  - dcat-ap
  - healthdcat-ap
authors:
  - name: Vasundra Touré
    orcid: 0000-0003-4639-4431
    affiliation: 1
    role: Conceptualization, Writing
  - name: Deepak Unni
    orcid: 0000-0002-3583-7340
    affiliation: 1
    role: Conceptualization, Writing
affiliations:
  - name: SIB Swiss Institute of Bioinformatics, Basel, Switzerland
    ror: 002n09z45
    index: 1
date: 26 March 2026
cito-bibliography: paper.bib
event: SWAT4HCLS2026
biohackathon_name: "SWAT4HCLS Biohackathon 2026"
biohackathon_url: "https://www.swat4ls.org/swat4hcls-biohackathon-2026/"
biohackathon_location: "Amsterdam, The Netherlands"
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/deepakunni3/from-dcat-to-healthdcat-ap-comparative-analysis
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Vasundra Touré \emph{et al.}
---

# Abstract

This project explores the landscape of healthcare metadata catalogs across Europe by comparing their underlying schemas. Participants will analyze similarities and differences among national implementations of DCAT-AP and HealthDCAT-AP, identifying both standardized areas and opportunities for improvement.

The work responds to challenges in discoverability and interoperability of healthcare datasets caused by divergent metadata standards and national adaptations. By collecting and examining schemas from multiple European initiatives, participants will map structural differences, overlapping concepts, and missing terms using established comparison frameworks and mapping tools.

Expected outputs include a comparative overview of healthcare metadata schemas, visual maps, gap analyses, and concrete recommendations for harmonization, potentially including a minimal convergent metadata schema. All results will be made openly accessible and collated for publication following the hackathon.


# Introduction

## Scope and Coverage

The comparative analysis encompasses seven metadata schemas and specifications. Together, they represent a cross-section of European and international initiatives aimed at making health and research data more discoverable, interoperable, and reusable.

- [Data Catalog Application Profile (DCAT-AP) 3.0](https://semiceu.github.io/DCAT-AP/releases/3.0.0/): The foundational European application profile of W3C DCAT, maintained by the EU Publications Office and SEMIC. It defines a common vocabulary for describing public sector data catalogs and datasets across EU member states, serving as the baseline from which most domain-specific profiles in this comparison are derived.

- [HealthDCAT Application Profile (HealthDCAT-AP) Release 6](https://healthdataeu.pages.code.europa.eu/healthdcat-ap/releases/release-6/index.html): A health-domain extension of DCAT-AP developed under the European Health Data Space (EHDS) initiative. It introduces health-specific metadata requirements such as population coverage, data sensitivity, coding systems used, and regulatory compliance attributes relevant to secondary use of health data.

- [DCAT Application Profile for Switzerland (DCAT-AP CH) 3.0](https://www.dcat-ap.ch/releases/v3/3.0.0.html): The Swiss national adaptation of DCAT-AP, aligned with opendata.swiss and the Federal Statistical Office requirements. While largely conformant with DCAT-AP, it introduces Swiss-specific controlled vocabularies, multilingual support obligations (DE, FR, IT, RM), and national governance constraints.

- [FAIR Data Point specification v1.2](https://specs.fairdatapoint.org/fdp-specs-v1.2.html): A community-driven specification for exposing machine-readable, FAIR-compliant metadata via a standardized REST API. Built on DCAT and Dublin Core, FDP defines a layered metadata model and places particular emphasis on automated discoverability and FAIR principle compliance as first-class requirements.

- [HealthRI Metadata Schema 2.0](https://github.com/Health-RI/health-ri-metadata): Developed by Health-RI, the Dutch national health data infrastructure. This schema extends DCAT-AP and HealthDCAT-AP to support interoperability across Dutch health research cohorts, biobanks, and registries, with a focus on findability within federated health data networks.

- [SPHN Metacat Schema 0.1.0](https://sphn.gitlab.io/sphn-metacat-schema/): A metadata catalog schema developed within the Swiss Personalized Health Network (SPHN) for the SPHN Metadata Catalog. It is designed to describe clinical and biomedical catalogs and datasets while leveraging DCAT and HealthDCAT-AP.

- [NFDI4Health Metadata Schema v3.3](https://doi.org/10.4126/FRL01-006472531): Developed by the National Research Data Infrastructure for Personal Health Data in Germany (NFDI4Health). The schema targets epidemiological studies, clinical trials, and public health datasets, with rich provenance, study design, and data collection attributes that go beyond standard catalog metadata.


## Comparative Analysis

The comparative analysis was performed to identify and document alignment at three levels:

1. **Structure:** Identification of top-level structural patterns across schemas including how metadata is organized into classes or sections (e.g., catalog-level vs. dataset-level vs. distribution-level), and whether a hierarchical or flat model is employed. This level of analysis reveals whether schemas share a common architecture, regardless of differences in field naming or vocabulary.

2. **Fields:** Identification of metadata fields that are semantically identical, functionally equivalent, or partially overlapping across schemas. This includes mapping fields with different labels that capture the same information (e.g., `dct:title`, `schema:name`, and `rdfs:label` as title representations), as well as identifying fields that are present in some schemas but absent in others, which may indicate domain-specific requirements or gaps in cross-schema coverage.

3. **Value space:** Identification of similarities and divergences in the allowed values for fields that have been determined to be identical or equivalent at the field level. This includes comparison of controlled vocabularies, ontologies, coding systems (e.g., ICD-10-GM, SNOMED CT, LOINC), and enumerated value sets, as well as the degree to which these are formally specified, loosely recommended, or left to the implementers.


## Results

### Review of metadata schemas

We began with a systematic review of all seven metadata schemas, examining their structure. The first step was to identify which schemas share common structure, as this directly determines the feasibility and granularity of cross-schema alignment.

Six of the seven schemas, DCAT-AP 3.0, HealthDCAT-AP, DCAT-AP CH, FAIR Data Point, HealthRI, and SPHN Metacat Schema, are grounded in the W3C Data Catalog Vocabulary (DCAT), either as direct application profiles or as extensions. This shared lineage means they all organize metadata around a common set of core classes:

- **`dcat:Catalog`**: Describes the data catalog itself: its publisher, coverage, licensing, and the datasets it contains.
- **`dcat:Dataset`**: The primary unit of description, capturing what the data is, who produced it, under what conditions it was collected, and how it can be accessed.
- **`dcat:Distribution`**: Describes a specific, accessible form or serialization of a dataset, including format, access URL, and license information.

Beyond these three core classes, most DCAT-based profiles in this comparison also make use of supporting classes such as `dcat:DataService`, `foaf:Agent` (for publisher and creator description), `dct:Location` (for spatial coverage), and `dct:PeriodOfTime` (for temporal coverage). The degree to which these supporting classes are required, recommended, or optional varies across profiles and constitutes one of the key axes of structural divergence examined in this analysis.

The NFDI4Health Metadata Schema v3.3 stands apart as the only schema in this comparison that is not derived from DCAT. It follows an independent structural model tailored to the specific requirements. While some NFDI4Health fields are semantically mappable to DCAT-AP equivalents, the structural mismatch requires a different alignment strategy.


### Mapping of metadata fields across schemas


### Querying via shared metadata fields

## Discussion


## Acknowledgements

## References

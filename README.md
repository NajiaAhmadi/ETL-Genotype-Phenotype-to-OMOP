# ETL-Genotype-Phenotype-to-OMOP
Extract Transform Load (ETL) processes to write gene mutation data and phenotype data to OMOP CDM

The processes are initiated via the MAINJob.ktj which calls both MAINJob_DD.kjb and FILL-SOURCE_TO_CONCEPT_MAP.kjb. 

## Genotype

### Mapping Table

Within the Genotpye directory the file "20220504_Mappings.xlsx" contains all the semantic mappings of the genotype elements to OMOP Concept_ids and relevant tables. Additionally, the OMOP_tables_used file shows which OMOP tables were utilized to write the data. 

#### Dataset-A-Transformations

The MAINJob_DD.kjb is loading the PERSON.ktr first and then runs the CONDITION_OCCURENCE, MEASUREMENT, and OBSERVATION. It additionally, fills the SOURCE_TO_CONCEPT_MAP table and truncates the tables if necessary. 

For the Person table in OMOP Year_of_birth is calculated via substrating the given age from the year 2023. Patients with an Age = NA will be filtered out as OMOP does not accept it. 


type_concept_id is mandatory in Observation and Measurement and type_concept_id = 32810 is used as constant.

## Phenotype

This Transformation processes fill the SOURCE_TO_CONCEPT_MAP table with a set of concepts_ids from Human Phenotype Ontology (HPO). These concepts transform phenotypic data elements possible (We did not have data to test this transformation for this study).


# Customize your Rare Diseases Common Data Model

Here, we outline how to adapt the RD-CDM for use across various data and medical fields for rare diseases.

## 1. Use Case Definition 

Specify the modules required to explore the research hypothesis. Identify key elements within these modules that address the research question.

## 2. Stakeholder Engagement 

Communicate the necessary modules and elements with medical experts to assess their availability at each study site. Engage with data providers to ensure data can be 
automatically retrieved, possibly in standard formats like FHIR, or using terminologies such as SNOMED. Consult legal authorities to address the sensitive nature of medical data, ensuring adherence to ethical standards, data security, and privacy protection.

## 3. Diagnostic Entity Compilation
Collaborate with stakeholders to finalize a comprehensive or selective list of data elements after initial discussions.

## 4. Mapping Use Case-Specific Entities
Align individual data items with the RD-CDM's modules to standardize data across all study sites.

## 5. Data Transformation
Implement ETL processes, for instance, converting FHIR to OMOP format, to standardize data in modules like "Person", "Diagnosis", "Laboratory findings", "Procedure", and "Medications".

## 6. Handling Genotypic and Phenotypic Data

Use direct ETL processes from CSV to OMOP CDM for the "Genotype" and "Phenotype" modules.



# ETL-Genotype-Phenotype-to-OMOP
Extract Transform Load (ETL) processes to write gene mutation data and phenotype data to OMOP CDM

The processes are initiated via the MAINJob.ktj which calls both MAINJob_DD.kjb and FILL-SOURCE_TO_CONCEPT_MAP.kjb. 

## Genotype

### Mapping Table

within the Genotpye directory the file "20220504_Mappings.xlsx" contains all the semantic mappings of the genotype elements to OMOP Concept_ids and relevant tables. Additionaly, the OMOP_tables_used file shows which OMOP tables were utilized to write the data. 

#### Dataset-A-Transformations

The MAINJob_DD.kjb has is laoding the PERSON.ktr first and then runs the CONDITION_OCCURENCE, MEASUREMENT and OBSERVATION. It additionaly, fill the SOURCE_TO_CONCEPT_MAP table and truncate the tables if necessary. 

For Person table in OMOP Year_of_birth is calculated via substrating the given age from the year 2023. Patients with an Age = NA will be filtered out as OMOP does not accept it. 


type_concept_id is mandatory in Observation and Measurement and type_concept_id = 32810 is used as constant.

## Phenotype

This tranformation fills the SOURCE_TO_CONCEPT_MAP table with a set of concepts_ids from Human Phenotype Ontology (HPO). These concepts makes the transformation of phenotypic data elements possible (We did not have data to test this transformation for this study).



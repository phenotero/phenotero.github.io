---
layout: page
title: Obo2json
subtitle: Transforming an ontology into a library
---

Our _obo2json_ converter is written in Java and can be obtained from our [GitHub repository](https://github.com/phenotero/obo2json). 

In a digital bibliography, entries must have values for specific fields such as title, author and type. For Phenotero, each ontology class is defined as an “entry-dictionary” type, to better distinguish it from articles, books, etc. This reference-type is rarely used in biomedical articles and should hence not interfere with other Zotero capabilities. The ontology IDs are stored in the container-title field and the synonyms under author, as this field allows to have multiple entries per item. The exact mapping between OBO fields and JSON-format for Zotero is described in the following Table:


| Bibliography field        | Value of ontology class           | Example value  |
| ------------- |-------------| -----|
| type      | always “entry-dictionary” | entry-dictionary |
|title     | primary label       |   Abnormality of the kidney |
| container-title | OBO-ID      |    HP:0000077 |
|id | PURL      |    http://purl.obolibrary.org/obo/HP_0000077 |
| author | List of synonyms and definition (one author per item)      |    “renal anomaly”, “kidney disease”, “An abnormality of the kidney."|




















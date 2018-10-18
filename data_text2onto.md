---
layout: page
title: Text2Onto
subtitle: Converting your documents into a phenotyping database
---

This tool has been created for the situation when you have created a set of text documents and have used Phenotero to annotate HPO or MONDO entries within the texts. Now, you might want to perform sophisticated analyses using your data or exchange the ontology references with a third party.

Our software _Text2Onto_ extracts ontology terms from all your documents and creates a tab-separated file of the form:

```

/patient_132.docx	HP:0000232,MONDO:0010561,HP:0000767,HP:0010864
/patient_4322.odt	HP:0000077,HP:0000767
/rare/patient_66322.docx	HP:0000232,HP:0000767,HP:0010864,HP:0000445
/rare/lastyear/patient_3.docx	HP:0000232,MONDO:0010561,HP:0000767,HP:0000445
/lastyear/patient_3322.docx	MONDO:0009162,HP:0000773,HP:0000774 
```

This can then be used for any downstream analysis like patient clustering etc.

Our software is freely available at our [GitHub repository](https://github.com/phenotero/text2onto).


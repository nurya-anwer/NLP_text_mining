# NLP_text_mining
First, let me introduce the background of this research project:
•	Cancer is the leading cause of death in the pediatric population.
•	An estimate 400,000 children and adolescents aged 0-19 develop cancer. 
•	Pediatric cancer types, molecular features, and pathogenesis can differ from adults. 
                                           So, Data analysis of pediatric cancer and relevant molecular targets are needed,  to facilitate the development of new drugs for safe and effective pediatric cancer therapy.  The Benefits include:
1)	Informing therapeutic strategies for pediatric cancer treatment
2)	Increase in cure rates 
3)	Improving the quality of life of children with cancer
4)	Help policy decisions. 
•	The Pediatric Molecular Target List (PMTL) was created in 2018 by the Food and Drug Administration (FDA) to facilitate pediatric oncology drug development
1)	This list consists of over 200 targets that show evidence of impacting the growth or progression of at least one pediatric cancer. 
2)	This list is required to be updated regularly and is currently updated manually
To reduce the manual curation required for PMTL updates, this project uses Linguamatics, a rule-based natural language processing (NLP) software to develop and improve a text-mining algorithm to identify molecular targets relevant to pediatric cancer. A original text-mining query was developed in 2019 to identify molecular targets associated with pediatric cancer in MEDLINE abstracts, and this study integrates new phrase patterns and cancers to increase performance.
•	This algorithm will provide target information to assist with PMTL updates and facilitate drug development
In this study, the materials and methods we used were:
•	1 `1Linguamatics OnDemand which is rule-based NLP software, was used to develop the query and extract molecular targets related to pediatric cancer
•	The MEDLINE abstracts index in Linguamatics was used for query development and it is also data and information resource to identify molecular targets associated with pediatric cancer
•	figure 1 shows the workflow for query development and evaluation process.                                                                                                                                                                                                                                                                                                                                                                                                                                                              
•	 
•	The first steps is the evaluation of text trends to identify rules.  eg: (phrase spacing, trigger words, etc)
As we know: Natural language processing (NLP) is the ability of a computer program to understand human language as it is spoken and written. It is a component of artificial intelligence. There are many different natural language processing algorithms, but two main types are commonly used: Rules-based and Machine learning-based. And in order to answer our sientific question:  
The original query was developed in 2019 by manually identifying “rules” from relevant abstracts for 50 targets on the PMTL. 
These 50 targets were used to validate the query once it was developed
Rules include:
1.	A gene and pediatric cancer within 20 words and within the same sentence
2.	A “Gene-Disease” linker between the gene and cancer
An ontology built into linguatics with relation words and pharases. For example : affect, associate, etc)
3.	Negation of medical terms that share the same abbreviation of a gene
For example: （BMP: Basic metabolic panel in medical abbreviation. BMP: Bone Morphogenetic Protein）
MedDRA terms were also nageted to prevent the query from incorrectly identify medical terms that share the same abbreviation or synonym of gene. 

Updates were made to enhance performance, including:
Negation of additional medical terms
For example:  “primary”, “care”, “providers”---to exclude irrelevant ariticles
========--For example: neuroblastoma cell lines are used to study Alzheimers disease.
 We also 8adjust Property panel disambiguation from 12 to 50(we can control whether or not matches related to these terms appear in the results by specifying higher disambiguation threshold. 
•	Considering Druggable tumor-specific molecular targets are constantly being discovered. And also considering the different molecular targets corresponding to different pediatric cancer, we summarize the common and uncommon pediatric cancer names and add it to the query. For example: including childhood atypical teratoid/rhabdoid tumor, astrocytoma, ependymoma, choroid plexus neoplasms, craniopharyngioma, germinoma, childhood nongerminomatous germ cell tumor. They were not included in the original query. Considering that rhabdomyosarcoma can occur at any age, it was removed from the section on cancers that only occur in children and added to cancers that can occur at any age. Then the algorithm searched for “child*” or “pediatric” within 20 unordered words of the gene-cancer association.
For Query texting: 
The query was tested using targets and abstracts that are currently on the PMTL as well as new targets found in medline abstract. 3 algrizom were used for query texting.
For Test 1: The remaining targets on the Pediatric Molecular Target List were used to ensure the query was not overtrained on the validation set. (Retrieval of current PMTL targets (Table 1))
Test 2: Abstract-gene pairs were curated to evaluate true/false positives and true/false negatives. (Evaluation of 100 current PMTL abstracts (Table 2)) I will explain its results in the Results section.
Test 3: All genes in the Entrez gene database were searched across all MEDLINE for any abstract that indicates targets associated with a pediatric cancer to identify new targets that may be relevant for the PMTL (Evaluation of new targets retrieved from MEDLINE (Figure 2))
For Statistical Analysis:
Sensitivity, specificity, and precision were calculated and compared to prior query versions
Our last step is Performance evaluation via Manual curation
•  Three team members manually reviewed the new molecular targets identified by the query in Test 3. 
•  An annotation protocol was created to find the molecular targets that related to the pediatric cancer, (1. A gene/protein that directly relates to cancer emergence and/or progression (“therapeutic target”) , has trigger words such as Association, role, etc. 2. A gene/protein that has prognostic significance in pediatric cancer (“prognostic biomarker”) 3. A gene/protein that helps with diagnosis or classification of pediatric cancer (“diagnostic biomarker”) 4. Alterations in expression of pathway/downstream genes 
ensure agreement on true and false positives, and interrater reliability was calculated
•  Based on the annotation protocol , pediatric cancer relevant Positive targets were classified as a “therapeutic target”, “prognostic biomarker”, “diagnostic biomarker”, or “other”

Result and discussion
Previous pediatric molecular target list contains over 200 targets. This project was developed and updated with a standardized text-mining algorithm with an established accuracy and high reproducibility that will allow us to update the list.
We did Comparison of the number of current PMTL genes returned by the original and updated queries. 
Based on Test 1result: Retrieval of current PMTL targets, From the table 1 we can see Returned(true positive) is 90 and Omitted (false negative) is 30.  So we can see that the number of current genes retrieved by the updated query in MEDLINE was less than the original query. This could be due to more stringent negation criteria.

Based on the Test 2 result : we use One hundred abstracts on the current PMTL were curated to evaluate query performance.  . We can see from the  (Table 2) The precision of the current version is near 100%, an increase of approximately 10% compared to the previous query, and specificity is near 100%. Which means that the updated query would not erroneously classify any unrelevant abstracts as relevant abstrats. That is good. However, The sensitivity is 69%,  less compare to the original query sensitivity which meaning some relevant abstracts were missed.

When Test3 query were run. When all of MEDLINE was searched, a total of 3967 new molecular targets that are not currently on the PMTL were retrieved. This is a very exciting result. Three team members manually reviewed the new molecular targets identified by the query in Test 3. And also, 
In order to assess the performance of the reviewers and how well they agree with each other.
We also did the Interrater reliability ----Cohen's kappa. It ranges from 0 to 1, and 0 would indicate basically random assignment of T/F by the reviewers and 1 would indicate that the reviewers are perfectly in agreement. 
From the table3 we can see our cohen’s kappa is over 0.7 between the reviewers. Which means the substantial agreement. 

After manual curation completed which is used to determine the performance of the algorithm and identify new molecular targets for the PMTL, there are 2142 newly discovered pediatric cancer markers: among them ｆｒｏｍ　ｔｈｅ　ｆｉｇｕｒｅ２　ｗｅ　ｃａｎ　ｓｅｅ　129 (6%), ｉｓ　diagnostic biomarkers ．　ａｎｄ　366(17%)　ｉｓ　prognostic biomarker, 250 (12%)other type of biomarker, and 1397 (65%)ａｒｅ　potential therapeutic targets that should be further evaluated for inclusion on the PMTL. ｗｅ　ａｌｓｏ　ｆｉｎｄ　overlap among the different biomarker group. 51 targets are Therapeutic and pronostic biomarkers. 11 targets are diagnostic biomarkers and pronostic biomarkers. 11 targets are Therapeutic and diagnostic biomarkers. With further filtering and prioritization, the results of this query will decrease the manual labor required to update the PMTL and aid as a reviewer tool during receipt and review of pediatric oncology studies.

Conclusions:
This project updated a standardized text-mining algorithm for molecular targets in pediatric cancer. Compared to the previous query version, more new pediatric cancer-related molecular targets were discovered.
The updated query demonstrates improved precision and specificity but may miss relevant abstracts. There is still a lo　of room for query updates.
Further updates to the query will aim to improve the sensitivity
Minimizing false positives will reduce the need for manual curation when updating the PMTL, provide evidence-based information to FDA oncology reviewers, and guide future pediatric oncology research. . After manual curation completed which is used to determine the performance of the algorithm and identify new molecular targets for the PMTL, there are 2142 newly discovered pediatric cancer markers: 129 diagnostic biomarkers, 366 prognostic biomarker, 250 other type of biomarker, and 1397 potential therapeutic targets that should be further evaluated for inclusion on the PMTL. With further filtering and prioritization, the results of this query will decrease the manual labor required to update the PMTL and aid as a reviewer tool during receipt and review of pediatric oncology studies
Lastly I would like to express my gratitude to my mentor for his supportive, helpful and patient guidance, and secondly I would like to thank Raajan Naik (OTS/OCP) for developing the original query modified in this project and Terry Tsui (OND/ORO) for her valuable insight and suggestions for improvements.  

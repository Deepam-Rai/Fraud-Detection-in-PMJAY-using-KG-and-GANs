# Fraud-Detection-in-PMJAY-using-KG-and-GANs
This work was done as the final year project for my MSc. in Data Science and Computing under the supervision of Sri. P. Sunil Kumar, Asst. Professor DMACS SSSIHL. It is the final part of a three part project and deals with detecting possible frauds in relevant domains using GANs and KG. Specifically Pradhan Mantri Jan Arogya Yojana (PM-JAY), world's largest health insurance/assurance scheme, by the government of India is chosen.


----
## About
This work demonstrates the possible use of an expert-system approach for fraud detection in the PM-JAY scheme. This merges rule-based with model-based fraud detection, getting best of both. Graph Neural Network model has been trained on the real PM-JAY data which has achieved considerable performance. Generative Adversarial Networks have been used to develop synthetic fraud data and also non-fraud data where the data was less in proportion or was not allowed to be publicly exposed. Further an open source python library PyNeFrauds has been developed to help automate major parts of the process.


----
## Result
We went through NHA's released guidelines on official PM-JAY portals and constructed fraud detection logic for available PM-JAY data. We also constructed ontology for fraud detection in PM-JAY based upon which the knowledge graph schema was constructed. Based upon the logic deduced from Anti-Fraud guidelines we detected some possible fraud in our data.  

Since the given PM-JAY data contained many sensitive beneficiary details we collaged many techniques while handling the data and during demonstration so as to not expose these sensitive data. Synthetic data generation played a major role here.  

We used CTGAN architecture which yielded synthetic data of high fidelity. The generated data was 100% synthetic with none being copied from original data.  

We found no open source library that integrated graph databases, specifically neo4j, with deep learning techniques. To fill this gap we developed the PyNeFrauds library that integrates Python Pytorch’s torch_geometric library with Neo4j for fraud detection.

----
## Links
 PyneFrauds library: https://github.com/Deepam-Rai/PyNeFrauds 

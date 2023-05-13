# Fraud-Detection-in-PMJAY-using-KG-and-GANs
Detecting possible frauds in relevant domains using GANs and KG. Specifically Pradhan Mantri Jan Arogya Yojana (PM-JAY), world's largest health insurance/assurance scheme, by the government of India is chosen.


----
## Abstract
Advancement in technology has brought information and immense computation power to
our fingertips. But access to immense information doesn't necessarily mean that the masses will
be updated and informed, rather they are being misinformed and misled greatly. The deficiency
of understanding and analyzing of these information has facilitated the commitment of
fraudulent activities. The project of which this particular project is the final part aims to take a
step against this issue by providing the information to masses in easily comprehensible form of
knowledge graphs and utilizing the same for detection of frauds in the real world data. To
achieve this the project focuses on PM-JAY, the world's largest social healthcare scheme
launched by the government of India.  

This final part proposes an expert-system approach for fraud detection in the PM-JAY
scheme. This merges rule-based with model-based fraud detection, getting best of both. Initially,
the rules for rule-based are provided by the domain experts. The model is trained on detected
frauds and an additional gain is that the model can adapt and learn to the fraud patterns which are
indiscernible in rule based systems. And further its output can supplement the rule-based system
further. The experimentation and the results of this project shows that such a system can be
implemented for PM-JAY. Graph Neural Network model has been trained on the real PM-JAY
data which has achieved considerable performance. Generative Adversarial Networks have been
used to develop synthetic fraud data and also non-fraud data where the data was less in
proportion or was not allowed to be publicly exposed. Since GANs learn the distribution of true
data, this generated data too follows real data as closely as possible. Further an open source
python library PyNeFrauds has been developed to help automate major parts of the process.



----
## Result
We went through NHA's released guidelines on official PM-JAY portals and constructed fraud
detection logic for available PM-JAY data of Sathya Sai District. We also constructed ontology
for fraud detection in PM-JAY based upon which the knowledge graph schema was constructed.
Based upon the logic deduced from Anti-Fraud guidelines we also detected some possible fraud
in our data.  

Since the given PM-JAY data contained many sensitive beneficiary details we collaged many
techniques while handling the data and during demonstration so as to not expose these sensitive
data. Synthetic data generation played a major role here.  

This project also shows that it is very much practical to generate tabular data for the PM-JAY
scheme. We used CTGAN architecture which yielded synthetic data of high fidelity. The
generated data was 100% synthetic with none being copied from original data.  

From literature review we came to know rule based systems and model based systems were used
to detect frauds. However we found no open source library that integrated graph databases,
specifically neo4j, with deep learning techniques. To fill this gap we developed the PyNeFrauds
library that integrates Python Pytorch’s torch_geometric library with Neo4j for fraud detection. It
is suitable for an expert-system fraud detection framework.

----
## Links
 PyneFrauds library: https://github.com/Deepam-Rai/PyNeFrauds  

#TODO readme

# Assigning unique id to all nodes
This is required because in the COO edge matrix, we need unique identifieres for source and destination. If the nodes of different types are having same primary key, then it might be difficult.  

Fow now setting the unique NodeID that neo4j uses, as unique ids.
```
CREATE CONSTRAINT FOR (n:Label) REQUIRE n.project_id is UNIQUE

MATCH (n) SET n.project_id = id(n)
```

# To save the output to files
Set:  
apoc.conf file: (right click on database; go to folder - neo4j installation folder;)
```
apoc.export.file.enabled=true
apoc.export.file.directory=/home/msc2/downloads/neo4j_files
```
By default files are stored in `import` folder of installation folder.


# Getting embeddings

## FastRP Embedding
1)
```
CALL gds.graph.project(
	'projectionName',
	'*',
	'*'
)

CALL gds.fastRP.write(
	'projectionName',
	{
		writeProperty:'fastRP_2',
		embeddingDimension:7,
		iterationWeights:[3.0,1.0],
		nodeSelfInfluence:1.0,
		randomSeed:13
	}
)
```

## Getting embedding csv files
Getting csv file for embedding:
```
CALL apoc.export.csv.query('MATCH(n:Patient) RETURN id(n) as neo_id, n.id as id, n.fastRPembedding as fastRPembedding', 'patients_embeddings.csv',{headers:'neo_id, id, Embedding'})

CALL apoc.export.csv.query('MATCH(n:Procedure) RETURN id(n) as neo_id, n.id as id, n.fastRPembedding as fastRPembedding', 'procedure_embeddings.csv',{headers:'neo_id,id, Embedding'})

CALL apoc.export.csv.query('MATCH(n:Treatment) RETURN id(n) as neo_id,n.fastRPembedding as fastRPembedding', 'treatments_embeddings.csv',{headers:'neo_id, Embedding'})

```


## Graph Sage

Project:
```
CALL gds.graph.project(
	'graphSage',
	{
		Patient: {
			properties: ['Rural','Urban','male','Female','age']
		},
		Procedure: {
			properties: ['Est_Amt','id']
		},
		Treatment: {
			properties: ["STATUS_Claim_Doctor_Approved","Preauth_status_Approved","STATUS_Preauth_Cancelled","STATUS_Repudiated_Claim_Appeal_Initiated","Preauth_status_Pending","STATUS_Claim_Doctor_Pending","STATUS_Discharge_Update","Admit_day","STATUS_CMC_SHAS_Approved","Admit_year","Admit_month","STATUS_Preauth_Rejected_by_Technical_Committee","Start_Date_day","Preauth_status_Cancelled","STATUS_Claim_Submitted","STATUS_Preauth_Terminated","Pre_Auth_Appr_Amt","STATUS_Treatment_Schedule_Update","STATUS_Preauth_Auto_Cancelled","STATUS_Preauthorisation_Pending","Preauth_status_Rejected","STATUS_Claim_Paid_SHAS","Start_Date_year","Start_Date_month","STATUS_Claim_Inprocess","STATUS_Claim_Doctor_Pending_Updated"]
		}
	},
	'*'
)
```

Train:
```
CALL gds.beta.graphSage.train(
	'graphSage',
	{
		modelName: 'graphSageModel',
		featureProperties: ['Admit_day', 'Admit_month', 'Admit_year', 'Est_Amt', 'Female', 'Pre_Auth_Appr_Amt', 'Preauth_status_Approved', 'Preauth_status_Cancelled', 'Preauth_status_Pending', 'Preauth_status_Rejected', 'Rural', 'STATUS_CMC_SHAS_Approved', 'STATUS_Claim_Doctor_Approved', 'STATUS_Claim_Doctor_Pending', 'STATUS_Claim_Doctor_Pending_Updated', 'STATUS_Claim_Inprocess', 'STATUS_Claim_Paid_SHAS', 'STATUS_Claim_Submitted', 'STATUS_Discharge_Update', 'STATUS_Preauth_Auto_Cancelled', 'STATUS_Preauth_Cancelled', 'STATUS_Preauth_Rejected_by_Technical_Committee', 'STATUS_Preauth_Terminated', 'STATUS_Preauthorisation_Pending', 'STATUS_Repudiated_Claim_Appeal_Initiated', 'STATUS_Treatment_Schedule_Update', 'Start_Date_day', 'Start_Date_month', 'Start_Date_year', 'Urban', 'age', 'id', 'male'],
		projectedFeatureDimension: 8,
		embeddingDimension: 8,
		randomSeed: 23,
		sampleSizes: [10,9]
	}
)
```

Stream Embed:
```
CALL gds.beta.graphSage.stream(
	'graphSage',
	{
		modelName: 'graphSageModel'
	}
)
YIELD nodeId, embedding
```

Write Embed:
```
CALL gds.beta.graphSage.write(
	'graphSage',
	{
		writeProperty: 'embeddingGraphSage',
		modelName: 'graphSageModel'
	}
)
YIELD nodeCount, nodePropertiesWritten
```

# Centrality
```
CALL gds.graph.project(

'centrality',

'*',

'*'

)
```

estimation
```
CALL gds.pageRank.write.estimate('centrality', {

writeProperty: 'pageRank',

maxIterations: 20,

dampingFactor: 0.85

})

YIELD nodeCount, relationshipCount, bytesMin, bytesMax, requiredMemory
```

stream:
```
CALL gds.pageRank.stream('centrality',

{dampingFactor: 0.65})

YIELD nodeId, score

RETURN nodeId, score

ORDER BY score DESC
```

write:
```
CALL gds.pageRank.write('centrality', {

maxIterations: 20,

dampingFactor: 0.65,

writeProperty: 'size'

})

YIELD nodePropertiesWritten, ranIterations
```



# visualizing sample graph
```
MATCH (n)

WITH n

LIMIT 10

MATCH (n)-[r]->(m)

RETURN n, r, m
```

```
MATCH (n)-[r]->(m)

WITH n, r, m

LIMIT 200

RETURN n, r, m
```

```
MATCH (n)-[r]->(m) WITH n, r, m, rand() AS random WHERE random < 0.01 RETURN n, r, m
```

----

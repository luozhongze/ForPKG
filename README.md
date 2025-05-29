# ForPKG: A Framework for Constructing Forestry Policy Knowledge Graph and Application Analysis (IJCNN2025)

<div align="center">

Jingyun Sun, Zhongze Luo*  <br>
🌲Northeast Forestry University, Harbin, China  <br>
*Corresponding author, <em>Member, IEEE</em>  <br>
Email: sunjingyun@nefu.edu.cn, luozhongze0928@foxmail.com <br>

</div>

A policy knowledge graph can provide decision support for tasks such as project compliance, policy analysis, and intelligent question answering, and can also serve as an external knowledge base to assist the reasoning process of related large language models. Although there have been many related works on knowledge graphs, there is currently a lack of research on the construction methods of policy knowledge graphs. This paper, focusing on the forestry field, designs a complete policy knowledge graph construction framework, including: firstly, proposing a fine-grained forestry policy domain ontology; then, proposing an unsupervised policy information extraction method, and finally, constructing a complete forestry policy knowledge graph. The experimental results show that the proposed ontology has good expressiveness and extensibility, and the policy information extraction method proposed in this paper achieves better results than other unsupervised methods. Furthermore, by analyzing the application of the knowledge graph in the retrieval-augmented-generation task of the large language models, the practical application value of the knowledge graph in the era of large language models is confirmed. The knowledge graph resource will be released on an open-source platform and can serve as the basic knowledge base for forestry policy-related intelligent systems. It can also be used for academic research. In addition, this study can provide reference and guidance for the construction of policy knowledge graphs in other fields.

<div align="center">

**Paper (journal version):** [https://arxiv.org/abs/2411.11090v1](https://arxiv.org/abs/2411.11090v1) <br>
**IJCNN 2025:** [https://arxiv.org/abs/2411.11090v2](https://arxiv.org/abs/2411.11090v2)

</div>

## Steps

### View the ontology on Protege

Ontology are saved in the ``ontology`` folder. After opening ``Protege.exe``, click File-Open and select ``on.rdf`` to open it

### View the knowledge graph on Neo4j

1. Node and relationship data are saved in the ``import`` folder in CSV UTF-8 format. Save this folder in the local Neo4j path, and then ForPKG can be stored and displayed.

```
D:\neo4j-community-5.18.1\import
```

2. Restart neo4j
On the computer, type ``cmd`` to enter the command line. Go to ``neo4j-community-4.3.18\bin``, type ``neo4j restart`` to restart neo4j. In the browser, type ``localhost:7474/browser/`` to enter neo4j.

```
cd D:\neo4j-community-5.18.1\bin
neo4j restart
```

3. Click the database icon and click ``:dbs`` of DBMS

## Explanation

```
Neo4j:

1. Import a specific entity type
LOAD CSV WITH HEADERS FROM 'file:///file_name.csv' AS line # file_name represents a specific entity type, and file_name.csv is the CSV file for that entity type  
MERGE (:file_name { ID: line.ID, name: line.name, LABEL: line.LABEL })

2. Delete a specific entity type  
MATCH (r:`file_name`) DETACH DELETE r  // file_name represents a specific entity type  

3. Create all relationships  
LOAD CSV WITH HEADERS FROM 'file:///roles.csv' AS row  // roles.csv is the CSV file containing all relationships  
MATCH (fromNode {ID: row.from}), (toNode {ID: row.to})  
CALL apoc.create.relationship(fromNode, row.relation, {}, toNode) YIELD rel  
RETURN rel  

4. Delete a specific relationship  
MATCH ()-[r:duty]-() DETACH DELETE r  

5. Delete all relationships  
MATCH ()-[r]-() DETACH DELETE r  

6. Display all entities and relationships  
MATCH (n) RETURN n  

The format of file_name.csv, with a total of 10 entity types  
ID,name,LABEL  

ORG.csv  
ID,name,LABEL  
ORG001,国家林业和草原局,ORG  
ORG002,各省级、市地级党委和政府,ORG  
...  

The format of roles.csv  
from,to,relation  

roles.csv  
ORG001,ACT001,duty  
ORG007,DOC001,publish  
CONC006,EXP_DEF010,define  
...
```
## Citation

```
@article{sun2024forpkg,
  title={ForPKG-1.0: A Framework for Constructing Forestry Policy Knowledge Graph and Application Analysis},
  author={Sun, Jingyun and Luo, Zhongze},
  journal={arXiv preprint arXiv:2411.11090},
  year={2024}
}
```

![png](./POSTER.png)

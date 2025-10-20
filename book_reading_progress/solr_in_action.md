2025/09/28  66

2025/09/29  94

2025/09/30  115

2025/10/09  130

2025/10/10  178

2025/10/13  plan/real   220/230

2025/10/14  plan/real   260/234

2025/10/17  plan/real   260/243

2025/10/20  skip to chapter 13 for cloud   start at 432   plan 476/476  completed

<img width="775" height="899" alt="image" src="https://github.com/user-attachments/assets/9ef833ff-851a-4537-b1aa-1c801aedd3a0" />
<img width="1177" height="528" alt="image" src="https://github.com/user-attachments/assets/2a162ec1-5f8c-4c72-9bc9-f90adf9315b7" />
<img width="637" height="399" alt="image" src="https://github.com/user-attachments/assets/18757696-4856-4792-a644-0c7957f1082a" />
<img width="802" height="446" alt="image" src="https://github.com/user-attachments/assets/08fcc87d-75ed-41bc-a215-1ff763a3f23c" />
<img width="773" height="623" alt="image" src="https://github.com/user-attachments/assets/c093178c-e59a-46e3-9bfa-f73902202fa3" />
<img width="682" height="642" alt="image" src="https://github.com/user-attachments/assets/b5bdda9e-70ad-45e7-aee0-f705cb2bad6d" />
<img width="1059" height="302" alt="image" src="https://github.com/user-attachments/assets/2d2d95a5-107a-4a99-a20d-170904588805" />
<img width="1173" height="759" alt="image" src="https://github.com/user-attachments/assets/be366e9c-4c6f-4ece-b6de-1f352a7d0897" />
<img width="1164" height="546" alt="image" src="https://github.com/user-attachments/assets/be589f7a-d3f1-4f69-a118-ede26997b12b" />
<img width="1197" height="852" alt="image" src="https://github.com/user-attachments/assets/81f0b6fd-bc89-43e3-a26d-1f5fcb325476" />


1. **Term frequency (tf)** is a measure of how often a particular term appears in a matching document, and it’s an indication of how “well” a document matches the term
2. **Inverse document frequency (idf)** a measure of how “rare” a search term is, is calculated by finding the document frequency (how many total documents the search term appears within), and calculating its inverse
3. **Precision** measures how correct each of the results being returned is, **Recall** is a measure of how thorough the search results are
4. **A denormalized document** is one in which all fields are self-contained within the document, even if the values in those fields are duplicated across many documents. 
5. In SolrCloud, an index split across multiple nodes is called a **collection**
6. **every shard must have an active server for distributed queries to work. If a shard does not have an active server, you cannot query Solr!!!**
7.  Sharding breaks a large index into multiple smaller indexes, which allows you to operate massive indexes that cannot fit on one server and parallelize complex query execution and indexing operations.
9.  Replication creates additional copies of a Solr index across multiple servers to add redundancy in case of failures. With multiple copies of each document in your index, Solr remains operable if one of the copies fails.
10. Replication also helps increase the number of queries an index can execute concurrently. A distributed query gets sent to one replica per shard, so it follows that if
you have ten replicas per shard, you can execute roughly ten times more queries concurrently.
11. To ensure that Solr continues to serve queries, SolrCloud supports redundancy by having multiple replicas per shard. To ensure that Solr continues to serve update requests (indexing), SolrCloud can automatically failover to select a new shard leader if the current leader fails.
12. Solr 4 does not have the concept of configurable consistency levels; a write must succeed on all active replicas of a shard. But Solr only considers active and recovering replicas when determining if a write succeeds. It does not consider an offline replica to need the update, as that will be addressed once the failed replica recovers, using a built-in recovery process. Put simply, Solr will continue to accept writes as long as there is one active host per shard.
13.  SolrCloud currently has zero tolerance for weak consistency; the write must succeed on all replicas for a shard.
14.  a **Solr core** is a uniquely named, managed, and configured index running in a Solr server; a Solr server can host one or more cores. A core is typically used to separate documents that
have different schemas.
#### new words
adage 
tweet

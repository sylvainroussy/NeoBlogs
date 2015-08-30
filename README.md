# Moving relationships

## introduction

A graph database is not a simple way to store connected data, it's also a powerful tool for managing dynamic relationships between data. 
And because relationships are natively implemented in Neo4j, we can use them as a simply way to identify a group of connected nodes. But it's not the only usage we can do of them.
It seems many use cases where Relationships move between nodes in subsequent queries. Theses relationships are specialized to store a particular state for a sub graph. 

## Relationship as a pointer

Our first sample to observe this behaviour is the famous Linked List. A linked list is a list where each member is ordered according to a relative position compared to the others elements.
First we need to create a `:LIST` node with three `:ELEMENT`linked to it.

    MERGE (elem1:ELEMENT{name:"elem1"})-[:IS_MEMBER_OF]->(list:LIST)
    MERGE (elem2:ELEMENT{name:"elem2"})-[:IS_MEMBER_OF]->(list)
    MERGE (elem3:ELEMENT{name:"elem3"})-[:IS_MEMBER_OF]->(list)
    
![Fig1. The list with elements](./blog1.png "Fig1. The list with elements")

Then we need to rely theses elements in an relative ordered way (the initial position is not necessary important, we choose here to match elements ordered by name property) :

    MERGE (elem:ELEMENT)-[r:IS_MEMBER_OF]->(list:LIST)
    WITH elem ORDER BY elem.name ASC
    WITH COLLECT(elem) AS elems
    FOREACH (n IN RANGE(0, LENGTH(elems)-2) |
    FOREACH (prec IN [elems[n]] |
    FOREACH (next IN [elems[n+1]] |
    MERGE prec-[:NEXT]->next)))



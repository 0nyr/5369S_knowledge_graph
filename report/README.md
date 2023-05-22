
# Latex

### compiling

`latexmk main.tex`

### compiling glossary / acronyms

`pdflatex main.tex`

`makeglossaries main`

`pdflatex main.tex`

# What is a KG?

## intro
> include the basic idea presented in the papers

Reading of 3 differents articles, mainly based on (KG21)(.


## development
> summarize the papers

##### what is KG

########## knowledge & graph
Not easy to define what knowledge is, so focus on "explicit knowledge": "something that is known and can be written down" (p4), composed of statements such as sentences, that are essentially sequences of words that draw relationship between concepts and data.

Graph theory: Theory ranging between computer science and mathematics that interests itself to the study of graphs. A graph is a kind of data structure consisting of nodes (aka vertices) and edges (arcs) that connect pairs of nodes. Based on the field and the shape of the graph, many properties can be deduced such as connectedness, cyclicity, planarity, as well as the presence of specific substructures like cliques or independent sets. These properties can provide valuable insights into the nature and characteristics of the system or network being modeled, enabling more effective analysis and decision-making. This theory is used to model and analyze various types of relationships and structures in a wide range of fields, including computer networks, social networks, biological networks, and many others.

Knowledge graph?: "we define a knowledge graph as a graph of data intended to accumulate and convey knowledge of the real world, whose nodes represent entities of interest and whose edges represent potentially different relations between these entities." (p3).

########## basic understanding
"At the foundation of any knowledge graph is the principle of first modelling data as a graph" (p4)

"Graphs offer a flexible way to conceptualise, represent, and integrate diverse and incomplete data." p5

"Knowledge graphs use a graph-based data model to capture knowledge in application scenar-
ios that involve integrating, managing and extracting value from diverse sources of data at large scale (p2)"

"has a number of benefits when compared with a relational model or NoSQL alternatives" p2
data to evolve in a more flexible manner p2

flexible way to organize data (not hierarchical, can represent incomplete information, no need for a precise schema 

########## types of KG
different types of graphs:
NB: "data can typically be converted from one model to another; in our view, a knowledge graph can thus adopt any such graph data model" (p6)
* Directed Edge-labelled Graphs (DEL): the classic graph, set of nodes and edges that connect the nodes with in certain way. RDF is a popular DEL data model.
* Heterogeneous Graphs: where each node and edge is assigned one type (p5), allow for partitioning nodes according to their type (for ML) (p6)
* Property Graphs: allows a set of property–value pairs and a label to be associated with nodes and edges (think of it as a kind of DB tables). Used in Neo4j (p6), great flexibility but harder to handle / query.
* Graph Dataset: set of named graphs, with a default graph with no ID. Useful when working with different sources.
* hypergraphs: allow edges that connect sets rather than pairs of nodes. 

##### storing and distributing KG
See (KG21, 2.1.6 p7)
relational databases either as a single relation of arity three (triple table),
as a binary relation for each property (vertical partitioning), or as n-ary relations for entities of a given type (property tables)
custom storage technique also exist

##### uses
open and entreprise KG
* open: BabelNet [90], DBpedia [76], Freebase [14], Wikidata [138], YAGO
* closed: Google KG
used for: Web search, commerce, social networks, finance, among others:
"Prominent industries using enterprise knowledge graphs include Web search, commerce, social
networks, finance, among others, where applications include search, recommendations, informa-
tion extraction, personal agents, advertising, business analytics, risk assessment, automation, and more besides (p4)

##### creation / extraction
"Creation often involves integrating data from diverse sources, including direct
human input; extraction from existing text, markup, legacy file formats, relational databases, other knowledge graphs; and so on." (p7)

##### querying
* SPARQL query language for RDF graphs
* Cypher [34], Gremlin [112], and G-CORE for property graphs

important concepts related to querying graphs
* Graph Patterns: a graph similar to the data being queried that can contain variables so that the it can be evaluated to retreive information from constants in the KG.
	* homomorphism-based semantics: multiple variables to be mapped to the same term
	* isomorphism-based semantics: requires variables on nodes and/or edges to be mapped to unique terms
* Complex Graph Patterns: combines several graph patterns with operators (union, filter, where...). Powerful but can generate duplicates in the answer.
* Navigational Graph Patterns: regular expression for matching paths with support to more complex querying similar to using regex (disjunction, concatenation, set of possible values...). Can generate infinite number of paths, so it can be better to only return nodes (finite number).

"Graph query languages may support other features beyond those we have discussed, such as aggregation, complex filters and datatype operators, sub-queries, federated queries, graph updates, entailment regimes, and so on." (p9)

########## validation
Graphs are poweful du to being able to represent incomplete data, however it is sometimes necessary to ensure certain properties in the graph depending on its uses.

important concepts related to graph validation:
* Shapes Graphs: selected subset of nodes, with specified constraints, usually expressed using UML diagrams (which is by itself a kind of property graph).
	* open shape: "allows the node to have additional properties not specified by the shape" (p10)
	* closed shape: "no possible additional properties for target nodes".
* Conformance: "A node conforms to a shape if it satisfies all of the constraints of the shape." (p9). A valid graph is such that every node conforms to a given shape. Different shape langages extensions to RDF are available (ShEx, SHACL).
* context: every piece of information exists with respect to a context. The context, alonside with origin/provenance and time frame all define the "scope of truth" (p11). A context can be implicit or explicit. 
	* Direct Representation: consider context information as any other data (for instance, include dates, origin...). Different onthologies can help to better define relevant way to include the context.
	* Reification: describe edges of a graph in another graph to represent the context. Several forms of reification exist such as "RDF reification, n-ary relations and singleton properties, [...] NdFluents" (p11)
	* Higher-arity Representation: modify the graph with context annotation direclty on the graph. Different approaches exists like RDF*, (edges can be defined as nodes), named graph containing context, properties...
	* annotations: annotate directly edges or nodes with metadata, context informations or other useful related information. Several annotation model exists like Temporal RDF (time), Fuzzy RDF (degree of confidence)...
	* other more complex solutions exists like using subgraphs with partially ordered dimensions...

########## deduction and inference
Inference refers to the process of deriving or deducing new facts or knowledge from the existing data in the graph. This is typically achieved through logical reasoning based on the relationships and rules defined within the graph, or even context and additional external information.

"These deductions may serve a range of applications, such as improving query answering (deductive) classification, finding inconsistencies, and so on." (p13)

Inference in KGs is a powerful tool for enriching the graph with additional information, improving the quality of search and query results, and enabling more sophisticated data analysis and decision-making processes. It's a fundamental aspect of many applications of KGs, including semantic search, recommendation systems, and natural language processing.

########## Onthologies
p13/37



## KG in real life
> Show example of how I use KG in my masterarbeit.

I have been using a Heterogeneous Directed Edge-labelled Graph for representing the heap-dump memory of different versions of OpenSSH. Each node represents an annotated block of bytes. The annotation is encapsulated in a type that can represent Data Structures, SSH Keys, pointers and so on. Thoses types are then being used for generating samples and labels used in the feature engineering and ML part.

## points raised during presentation
> include the points raised in the seminar by the moderator (collaborate with the opponents if necessary)

## paper evaluations
> Identify strengths and weaknesses, question the assumptions, criticize the bad decisions in the papers

(KG21):
+ do not assume that readers have specific expertise on knowledge graphs.
+ meta-analysis, 13 external papers and books reviewed
+ extended online version
+ concrete examples (many) on GitHub: https://github.com/knowledge-graphs-tutorial/examples
- surface document, doesn't really goes into details
+ has "article structure" section
+ recent paper (2021)
+ provide some recommendations: "allows edges to be defined as nodes..." (p11)
- only focused on DEL graphs
- very little (5 lines) on KG creation or extraction, but well covered in extended version

## conclusion
> include the important results and conclusions




## bibliography
(KG21) [Hogan, Aidan, et al. &#34;Knowledge graphs.&#34; ACM Computing Surveys (CSUR) 54.4 (2021): 1-37](https://dl.acm.org/doi/abs/10.1145/3447772)

(KGKE22) [Knowledge Graphs and their Role in the Knowledge Engineering of the 21st Century](https://drops.dagstuhl.de/opus/volltexte/2023/17810/pdf/dagrep_v012_i009_p060_22372.pdf)

(CKG23) [Marvin Hofer, Daniel Obraczka, Alieh Saeedi, Hanna Köpcke and Erhard Rahm. "Construction of Knowledge Graphs: State and Challenges" (2023)](https://arxiv.org/pdf/2302.11509.pdf)






## TODO: go further
A number of systems further allow for distributing graphs over multiple
machines based on popular NoSQL stores or custom partitioning schemes [63, 146]. For further
details, we refer to the book chapter by Janke and Staab [63] and the survey by Wylot et al. [146] dedicated to this topic.





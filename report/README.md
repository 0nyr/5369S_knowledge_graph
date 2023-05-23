
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

########## Onthologies
p13/37
"In computing, an ontology is then a concrete, formal representation—a convention—on what
terms mean within the scope in which they are used" (p13)
Shared ontologies make KG that use them more interoperable, but many onthologies exists depending on the context and use cases: Web Ontology Language (OWL) by W3C (RDF compatible), Open Biomedical Ontologies Format (OBOF).

* Interpretations: The real-world knowledge we human understand is call the "domain graph". It's an abstract notion, contrary to KG that are concrete. So every KG can be interpreted (understood) by mapping its nodes and edges to entities and relations. But many interpretations are possible (depending on who reads the KG for instance).
* Assumptions: assumptions we make on KG is going to dictate how they can be interpreted
	* Closed World Assumption: "what is not known is assumed false" (p14)
	* Open World Assumption: "it is possible for the relation to exist without being described by the graph" (p14)
	* Unique Name Assumption: "no two nodes can map to the same entity" (p14)
	* No Unique Name Assumption: it is possible that two nodes designate the same entity.
Since KG are often incomplete, Open World Assumption and No Unique Name Assumption are generally the considered assumptions.
* Semantic Conditions: case-specific assumptions that can make reasoning and entailment in the graph easier, by stating that if certain patterns are respected, then we can deduce some knowledge from it.
* Individuals: refers to real life entities. It is possible to apply rules for instance to try to distinguish nodes that refer to similar or different entities
* Properties:  "terms that can be used as edge-labels" (p14). It's possible to define a range of caracteristics on properties, like range, domain, equivalence, inverse, disjoinction, transitivity, symmetricity, reflexiveness, multiplicity... A property can also be a part of a chain, "such that pairs of entities related by the chain are also related by the given property" (p15)
* Classes: regroupment of nodes under a similar type (basically another property). Classes can also have caracteristics like equivalence, intersection, disjunction, complement... Classes can also have features with specified cardinality (think of it as Java classes or UML class diagram). One can also specify reasoning on classes, or rules 

Onthologies can be very complexe, with many more features like datatype facets ("defining new datatypes by applying restrictions to existing datatypes" (p15))

########## deduction, inference and entailment
> I have choosen to regroup some sections here
* Deduction: Process of deriving new data from what is already given and some implicit or explicit rules " allowing us to know more than what is explicitly given to us by the
data." (p12)
* Inference: Inference refers to the process of deriving or deducing new facts or knowledge from the existing data in the graph. This is typically achieved through logical reasoning based on the relationships and rules defined within the graph, or even context and additional external information.

"These deductions may serve a range of applications, such as improving query answering (deductive) classification, finding inconsistencies, and so on." (p13)

Inference in KGs is a powerful tool for enriching the graph with additional information, improving the quality of search and query results, and enabling more sophisticated data analysis and decision-making processes. It's a fundamental aspect of many applications of KGs, including semantic search, recommendation systems, and natural language processing.

* Entailment: deductive process where a relationship between statements or sets of statements where the truth of one statement or set necessarily implies the truth of another. By extension, "We say that one graph entails another if and only if any model of the for-
mer graph is also a model of the latter graph" (p17). In short, two graphs are entailed if they mean the same.
* Model-theoretic Semantics: Adding property axioms which define truth conditions, means that only certain interpretations become possible. "interpretations that satisfy a graph are called 'models' of the graph" (p16). 
* Reasoning: Once working with big graphs, the process of knowing if one graph entails the other second is undecidable. So we can only rely on practical algorithms whose properties depend on the KG and onthology, and that cannot be guarantied to be always correct of able to complete.
* Inference Rules: If-then (body-head) like statements with body and head being graph patterns. Predefined sets of rules exists for popular onthologies like "OWL 2 RL/RDF". Languages for expressing rules over KG also exists like Rule Interchange Format (RIF) or Semantic Web Rule Language.
* Description Logics (DLs): DLs comes from First Oder Logic (FOL), and are based on three types of elements:
	* Individuals: These are specific instances or objects, such as 'Santiago'.
	* Classes: (or concepts) categories or types of objects, such as 'City'.
	* Properties: (or roles), represent relationships between individuals, such as 'flight'.
DLs allow for making claims (known as axioms) about these elements. Axioms can be unary class relations on individuals (e.g., City(Santiago)) or binary property relations on individuals. Web Ontology Language (OWL) was heavily influenced by DLs, with OWL 2 DL language being a restricted fragment of OWL with decidable entailment.

########## inductive reasoning and learning
Inductive reasoning is a process that involves making generalizations based on observed patterns. This could involve using machine learning techniques to predict missing links or infer new knowledge. The paper also discusses the challenges associated with inductive reasoning, such as the difficulty of handling noise, incompleteness and uncertainty in the data.

Learning on graph is possible using a wide range of techniques.
* Learning from the Graph Structure: methods such as graph kernels, which are used to measure the similarity between different parts of a graph, and graph neural networks, which are used to learn representations of nodes, edges, or entire graphs. The paper also mentions the use of graph embeddings, which are vector representations of nodes or edges that capture their structural roles and relationships in the graph.
* Learning from the Graph Content: learning from the content of the graph, such as the labels on nodes and edges. It mentions methods such as label propagation, which spreads labels from labeled nodes to unlabeled ones, and semi-supervised learning, which uses a small amount of labeled data to guide the learning process. The paper also discusses the use of multi-modal learning, which combines different types of data (e.g., text, images, etc.) associated with nodes or edges.
* Learning from the Graph Context: learning from the context of the graph, such as the temporal or spatial information associated with nodes or edges. It mentions methods such as temporal graph neural networks, which model the evolution of graphs over time, and spatial graph convolutional networks, which capture spatial dependencies between nodes.


## KG in real life
> Show example of how I use KG in my masterarbeit.

I have been using a Heterogeneous Directed Edge-labelled Graph for representing the heap-dump memory of different versions of OpenSSH. Each node represents an annotated block of bytes. The annotation is encapsulated in a type that can represent Data Structures, SSH Keys, pointers and so on. Thoses types are then being used for generating samples and labels used in the feature engineering and ML part.

## points raised during presentation
> include the points raised in the seminar by the moderator (collaborate with the opponents if necessary)

## paper evaluations
> Identify strengths and weaknesses, question the assumptions, criticize the bad decisions in the papers

(KG21):
+ do not assume that readers have specific expertise on knowledge graphs, and as such can be very informative for readers that want to grasp a good overview of what are KG.
+ meta-analysis: 13 external papers and books reviewed
+ extended online version
+ concrete examples (many) on GitHub: https://github.com/knowledge-graphs-tutorial/examples
+ in-depth concept discussion: The paper covers many crucial complex topics with a deep understanding. It also discusses how these concepts are applied in the context of knowledge graphs.
+ has "article structure" section
+ still recent paper (2021)
+ Provide some recommendations: "allows edges to be defined as nodes..." (p11). Also provide useful bibliography and further readings for topics that are not covered in depth.
- Only focused on DEL graphs
- Focused on core theorical concepts: It would benefit from more practical examples or case studies showing how these concepts are applied in real-world settings.
- KG creation: very little (5 lines) on KG creation or extraction, but covered in extended version
- content complexity: While still comprehensive for newcomers, it is challenging for readers who are new to the field due to the complexity and profusion of topics discussed. The paper could benefit from a more gradual introduction to these complex topics.
- Imbalanced topic discussion: While some crucial topics for newcomers like KG creation are not covered, other more advanced ones are presented with a lot of details like inductive reasoning or learning methods such as graph kernels and graph neural networks. While these are important subjects, the choice for such a focus is odd.
- Lack of discussion on challenges: Too few discussions on challenges associated with  knowledge graphs, such as issues related to scalability, data quality, and the complexity of reasoning tasks.


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





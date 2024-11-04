

# Conceptual Knowledge

## Learning Outcomes

1. How are natural categories different from the classical approach?
2. Describe the components of the following approaches to knowledge representation:
	- prototypes
	- exemplars
	- feature comparison model
	- semantic network models
	- connectionist approach
3. Explain the pros and cons of each model.
4. What are some kinds of schemas? How do scripts and schemas affect memory?

---

## Categorization
- **category**: class of objects, associated on the basis of some relationship
- **concept**: mental representations of a category
	- depends on **generalization**: identifying features common to all members of a conceptual class
	- **discrimination**: notice differences between conceptual categories

Bruner, Goodnow, & Austin (1956): benefits of categorization:
- reduces ==complexity== of the environment
- means by which objects of the world are ==identified==
- reduces need for constant ==learning==
- allows us to decide what constitutes an appropriate ==action==
- enables us to order and relate ==classes== of objects and events

### Classical Approach

Assumptions:
- categorization based on lists of **defining features**: those that are necessary to the meaning of the item
	- e.g., a triangle is a closed, three-sided figure
- features are individually necessary and collectively sufficient

Pros & cons:
- [p] distinction between different categories is clear and logical
- [p] works for ==logical== categories:
	- e.g., geometric shapes, prime numbers
- [c] implies that all members are created ==equal==

### Natural Categories

Assumptions:
- groupings or clustering of objects or concepts that occur naturally in the real world
- ==fuzzy== borders; membership may overlap
	- e.g., what are the defining features for the concept ==vehicle==?

---

## The Prototype Approach

Eleanor Rosch [née Heider] (1973)

Assumptions:
- items are comprised of a list of features or attributes
- concept organization based on **prototype**: abstract, idealized item that is most typical category member
- **characteristic features**: describe the prototype, but are not necessary
- categorization of items is based on similarity to the prototype
- concepts are ==hirearchically== organized:

|       | animals | animals |
| ----- | ------- | ------- |
|       | ↙       | ↘       |
| birds | birds   | fish    |
| ↙     | ↘       |         |
| robin | bluejay |         |
|       |         |         |

- **==Superordinate== level** (e.g., -*fruit*-, -*animals*-)
	- largest categories
	- members of a category have few attributes in common
		- e.g., musical instruments
	- tends to be abstract

- **==Basic== level** (e.g., -*grapes*-, -*apples*-)
	- prototypes formed to represent the category
	- members of a category share many attributes, and are highly differentiated from other basic categories
		- e.g., guitar, piano
	- shows **==priming effect==**: response is faster if item is preceded by a similar item
		- e.g., judgments about specific apples are faster if preceded by -*apple*-, than by -*fruit*-
	- in general, people prefer to use basic-level names for things
	- ==Children== learn basic level objects first (-*dogs*-), before they categorize in superordinate (-*animal*-) or subordinate (-*collie*-, -*hound*-)

-  **==Subordinate== level** (e.g., -*Thompson seedless*-, -*Concord*-)
	- narrowest categories
	- less ==distinct== than basic categories
		- e.g., classical guitar, folk guitar
	- ==experts== prefer to use subordinate-level terms; greater expertise -> greater use of sub-subordinate terms (Johnson & Mervis, 1997)

Evidence:

- **==typicality== effect**: items differ in how well they represent a category
	- e.g., rank order these items in their category:
		- -vehicles-: car, elevator, sled, tractor, train
		- -clothes-: jacket, mittens, necklace, pajamas, pants
- **==family resemblance==**: each item has at least one shared attribute with another item in the category; is a kind of typicality
	- good members of a category share many attributes with members of the same category
	- but share few attributes with members of other categories

Rosch & Mervis (1975):

- generated list of category members
	- e.g., -*fruit*-: apple, banana, coconut, olive, orange, tomato
- asked participants to rate typicality of each member within category
	- e.g., apple as a member of -*fruit*-
- others listed attributes of category members
	- e.g., apple: red, sweet, crunchy, round
- strong correlations found between typicality rating and number of attributes shared by other category members
	- e.g., -*r*- = .85 for -*fruit*- (also, -*r*- = .88 for -furniture-, -*r*- = .91 for -*clothing*-)
- ==family resemblance== is important to typicality


brain activity : Kosslyn, Alpert, & Thompson (1995):

- participants placed in PET scanner
- saw picture of an item, and heard a word (e.g., “toy,” “doll,” or “rag doll”
- superordinate terms more likely to activate part of the ==prefrontal== cortex (language, associative memory)
- subordinate terms more likely to activate visual attention areas

Pros & cons:
- [p]  accounts for concepts representing loose groups
	- e.g., -*games*- - merely share a family resemblance
- [p]  allows for ==variability==
- [p]  explains how information is ==reduced== to a single, idealized abstraction
- [c]  but we also store ==specific== information about individual examples
- [c]  number of potential ==features== is very large (infinite?)
- [c]  what determines feature weights?
- [c]  how does expertise change categories?
- [c]  counterintuitively implies categories have fuzzy boundaries
---

## The Exemplar Approach

Assumptions:
- **==exemplars==**: members of a category that you have previously encountered (vs. prototypes, which are idealized)
	- e.g., -*dog*- concept is based on actual dogs you’ve seen
- first you learn specific exemplars of a category, then you classify new items based on their similarity to the exemplars

Heit & Barsalou (1996):
- asked participants for exemplars of various categories of animals
- measured exemplars’ typicality, and how typical the categories were of animals
- strongly correlated: -r- = .92
	- (==mammals== are most typical; ==microorganisms== the least)
- implication: our concepts are based on the most typical (i.e., exemplary) items

Pros & cons:
- [p]  accounts for typicality effect
- [p]  no lists of features needed
- [p]  no abstraction process needed
- [p]  allows for “==exceptions==” to categories
	- e.g., penguins as birds
- [p]  good for categories with ==few== members
- [c]  requires vast storage for individual members of large categories

---

## Feature Comparison Model

(Smith, Shoben, & Rips, 1978)

Assumptions:

- concepts represented as a set of features:

| **bird:** | **robin:** |
| --------- | ---------- |
| wings     | wings      |
| feathers  | feathers   |
| ...       | red breast |
| ...       | ...        |
- **==defining== features**: essential, required features of a concept; are at the top of the feature list
- **==characteristic== features**: descriptive, but not essential (“loosely speaking”); are at the bottom of the list
	- e.g., birds:
		- defining features = wings, feathers,...
		- characteristic features = fly, sing,...
- **==sentence verification== task**: measure RT to correctly respond, “A robin is a bird.”
- relations between concepts are computed based on shared features; more features -> slower RTs
- two-stage model:

|     |             |          |                                                             |       |              |
| --- | ----------- | -------- | ----------------------------------------------------------- | ----- | ------------ |
|     |             |          | Stage 1: compare --- features<br><br>(fast comparison)      |       |              |
|     |             | ↙        | ↓                                                           | ↘     |              |
|     | low overlap |          | medium overlap                                              |       | high overlap |
|     | ↓           |          | ↓                                                           |       | ↓            |
|     | ↓           |          | Stage 2: compare -------- features<br><br>(slow comparison) |       | ↓            |
|     | ↓           | ↙        |                                                             | ↘     | ↓            |
|     | “false”     | mismatch |                                                             | match | “true”       |

Pros & cons:

- [p]  typicality effects: faster RT when item is a typical member of a category
	- e.g., “A robin is a bird.” (faster than) “A penguin is a bird.”

- [p]  **==true/false== effect**: quick rejection of false sentences e.g., “A pencil is a bird.” (faster than) “A bat is a bird.”

- [c]  doesn’t explain **==category size== effect**: faster RT when item is member of a small category
	- e.g., “A robin is a bird.” (faster than) “A robin is an animal.”
	- small categories have -more- defining features -> -more- stage 2 processing -> -slower-

- [p]  can account for ==violations== of category size effect:
	- e.g., “Scotch is a liquor.” (slower than) “Scotch is a drink.”

- [c]  not all defining features of a category are necessary
	- e.g., “Is a robin with no wings still a bird?”

- [c]  features poorly ==Defined==; characteristic features have circular definition

---

## Semantic Network Models

Common assumptions:

- concepts represented in network of interconnected ==nodes==
- concept defined in terms of ==connections== to other concepts

**Hierarchical-Network Model** (Collins & Quillian, 1969)

![Hierarchical-Network model](PSYCH%20258/Attachments/p258s09-01.png)

Assumptions:

- ==node== represents a single concept
- concepts organized hierarchically
- pathways represent associations between concepts
- “==isa==” pathways: express category membership
- “==hasa==” pathways: express properties
- properties stored at the most general (“highest”) level possible, with no redundancy (**cognitive economy**)
- sentence verification via **==intersection search==**:
	- “A canary is a bird.”
	- “canary” and “bird” activated; activity spreads to neighbours
	- both spreads eventually intersect, allowing answer to be made

Pros & cons:

- [p]  cognitive economy:
	- e.g., “A bird has feathers.” (faster than) “A bird has skin.”

- [p]  corresponds well with category size effect:
	- e.g. “A canary...”

| **Category**       |          | **Property**   |          |
| ------------------ | -------- | -------------- | -------- |
| “...is a canary.”  | 1,000 ms | “...can sing.” | 1,350 ms |
| “...is a bird.”    | 1,200 ms | “...can fly.”  | 1,400 ms |
| “...is an animal.” | 1,300 ms | “...has skin.” | 1,500 ms |
- [c]  doesn’t explain violations of category size effect:
	- e.g., “A dog is a mammal.” (slower than) “A dog is an animal.”

- [c]  typicality effects (model predicts they should -not- be obtained):
	- e.g., “A robin is a bird.” (faster than) “An ostrich is a bird.”

**Spreading Activation Model** (Collins & Loftus, 1975)

![Spreading Activation model](PSYCH%20258/Attachments/p258s09-02.png)

Assumptions:

- not hierarchical
- link length represents degree of relatedness; search time depends on link length
- passive concepts not in working memory; active ones are
- **==spreading activation==**: activation of one node leads to (partial) activation of connected nodes
- degree of activation decreases over distance and time

Pros & cons:

- [p]  accounts for: category size effects (& violations), typicality effects
- [p]  Meyer & Schvaneveldt (1976):
	- **==lexical decision== task** (word/nonword):

| **Type of trial:** | **Prime** | **Target** | **RT**     |
| ------------------ | --------- | ---------- | ---------- |
| related prime      | “bread”   | “butter”   | 600 ms     |
| unrelated prime    | “nurse”   | “butter”   | ==670== ms |
- closely related concepts have shorter RTs
- **-------- ------- effect**: activation of a conceptual node facilitates retrieval of associated concepts or words

- [c]  difficult to falsify: what determines link length?

---

## Connectionist Approach

- a.k.a. Parallel Distributed Processing (PDP) or artificial neural network models
- classical approach: based on information & rules (serial approach)
	- e.g., mind is like a computer: data & programs

- ==Parallel==:
	- many (simple) processors working simultaneously
	- models are artificial neural networks, analogous to human brain
- ==Distributed==:
	- memory and information processing occur in the connections, not in storage locations (“connectionism”)
	- information is distributed across the entire network, not localized
- ==Processing==:
	- processing units = neurons; are interconnected
	- active unit may pass along its activity via connections,  excitatory vs. inhibitory
	- strength of connections may be modified--learning!
	- damage resistant: partial network may still solve problem

Jets & Sharks Example (McClelland, 1981):

- information can be stored in a table:

| **name** | **gang** | **age** | **education** | **marital status** | **occupation** |
| -------- | -------- | ------- | ------------- | ------------------ | -------------- |
| Art      | Jets     | 40s     | jr. high      | single             | pusher         |
| Lance    | Jets     | 20s     | jr. high      | married            | burglar        |
| Ralph    | Jets     | 30s     | jr. high      | single             | pusher         |
| Rick     | Sharks   | 30s     | high school   | divorced           | burglar        |
| Sam      | Jets     | 20s     | college       | single             | bookie         |
- or distributed in a network:

![network](PSYCH%20258/Attachments/p258s09-03.png)

Components:

- neuronally inspired
- **nodes**: processing units like neurons
- excitatory/inhibitory connections among nodes
- **==activation== rules**: specify conditions for activating a node
- **==learning== rule**: describes how connections can be changed, to improve performance

Pros & cons:

- [p]  biologically ==plausible==
- [c]  so far, fairly ==simple== (but increasing in complexity)
- [c]  as a model of a complex system becomes more complete, it becomes less understandable (==Bonini==’s Paradox, 1963)

---

## Schemas & Scripts

- contain generalized knowledge about things or events
- allow organization of objects & experiences
- kinds:
- **==scripts==**: sequences of actions for complex situations and events
- **==frames==**: for physical objects (room, desk, house)
- **==story== schemas**: setting, conflict, resolution, closing
- **==problem== schemas**: for typical structure of problems

### Scripts

Bower & colleagues (1979):

- participants were given texts over a dozen routine activities, including going to the dentist, a restaurant, or the doctor
- were later given a recognition test that included:
- sentences included in the text (e.g., “The doctor was very nice to him.”)
- unstated sentences that fit the script (e.g., “John took off his clothes.”)
- sentences of false, but plausible actions (e.g., “The doctor was not very rude to him.”)
- rated confidence that they had read the sentence on a 7-point scale
- results:

![scripts](PSYCH%20258/Attachments/p258s09-04.png)

- scripts help guide actions; may ---- -- details

### Characteristics of Schemas

Bransford & Johnson (1972): encoding

- participants read (vaguely written) paragraphs
	- e.g., about doing Laundry, Flying a Kite

- some were given topic sentence beforehand; had much better recall
- schemas add meaning, which aids encoding & remembering

Bartlett (1932): ==inferences==

- “The war of the ghosts” Native American story read by students in England
- reproductive memory was poor, because story/structure were unfamiliar
- recall included many reconstructive errors: story was combined with (or interpreted by) students’ existing schemas
- schemas show **==inferences==**: logical interpretations/conclusions made that are not part of original stimulus material

Brewer & Treyens (1981): ==memory== selection

- participants visited office for 35 seconds
- free recall of “everything you can remember about the room you were just in”
- good recall of objects consistent with “office” schema (e.g., desk, chairs)
- poor recall of inconsistent objects (e.g., picnic basket, ==wine bottle==)
- some false recall of consistent objects that were not present (e.g., ==books==, filing cabinet)
- schemas provide enhanced memory--for schema-consistent items

### Schemas Summary

- based on our general world knowledge and experiences
- active, constructive process for comprehension
- used at encoding, they ==increase== details remembered
- may ==bias== interpretation of ambiguous information
- may cause us to ------ inconsistent information

---

This document copyright © 2000-2024 Karsten A. Loepelmann. All rights reserved. Viewing this page is taken as acceptance of the [copyright agreement](https://sites.ualberta.ca/~kloepelm/copy.html).
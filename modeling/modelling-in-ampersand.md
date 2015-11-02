# Modeling in Ampersand


## What is a model about?
An ampersand model describes the rules, relations and concepts that define a business system. Using this specification, a software system can be built that can hold structured information as a set of facts. Based on the rules, the set of facts can be checked automatically to detect violations of rules. 

In an Ampersand model, interfaces can be defined too, enabling the definition of changes to the set of facts.

## Relations & Concepts
A fact is a statement that is True. *Joe Smith lives in New York* could be a fact. In this example, *Joe Smith* could be seen as an instance of a **Person** and *New York* as an instance of **City**. 

We can define the **relation** *lives in* between the **concepts** *Person* and *City* to hold facts about persons living in cities.  


## Rules
Every rule is denoted both as a statement in natural language (i.e. free text) as well as a formal expression. The Ampersand modeler is responsible that the semantics of both ways to express a rule is equivalent.

The formal expression of a rule uses relations that must be declared in the model. Ampersand will make sure that the types of the relations used in a rule are logically correct. Whenever the relations are populated with data, Ampersand will detect violations of any rule in the model. 

Basically, there are two distinct ways to handle violations of rules. Based on the way a rule is enforced, the rule is categorized in different ways:
 
 1. **Invariant**. A rule that is guaranteed to be true at all times. Whenever an action would cause a violation of the rule, that action is forbidden.  
 2. **Process rule**. A rule that may be (temporarily) violated. A violation of a rule will be signaled to the maintainer of that rule. It simply shows work that has to be done. 

In Ampersand, the default way of enforcement is as an invariant. A rule can be specified to be a process rule, by specifying what role should maintain the rule. 

## Interfaces
An interface is a mechanism to add or remove facts to the set of facts that is hold by the business system. 


 
 
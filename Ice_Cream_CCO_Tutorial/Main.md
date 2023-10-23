**Ice Cream Ontology:**

**An Introduction to Modeling with BFO and CCO**

_ **\*DRAFT\*** _

**10/15/2023**

Cameron More

National Center for Ontological Research

**Introduction**

The purpose of this tutorial is to familiarize knowledge engineers, ontologists, and data workers with core elements of ontology design in Basic Formal Ontology (BFO) and especially the Common Core Ontologies (CCO), a suite of mid-level modules that model 'human sized' entities (whereas many biomedical ontologies model microscopic, biological, or animal-sized domains).

This tutorial already assumes some basic understanding of what an ontology is, a controlled vocabulary of terms that model data to make it interoperable between systems, what classes and individuals are, and how to use some ontology editing software, Protégé or Mobi. To learn the BFO-CCO way of modeling, we will be constructing an Ice Cream Ontology, the natural next step after the popular Pizza Ontology, which is designed to help learn Protégé.

**Classes**

Since the world is filled with actions, and data about actions which have or will taken place, the CCO has designed a standard way of talking about processes in the world in the Event Ontology. The first heuristic CCO uses is that processes are often labeled with 'Act,' like 'Act of Speech,' or 'Act of Communication,' which, in English, offers more precision and clarity than the word 'process.' All events are subclasses of bfo:process, but the Act heuristic makes it more definite when things happen. Take, for instance, an Act of Aircraft Flight. It feels more definite when it occurs, namely when the wheels of the aircraft have left the ground; we may say that an Act of Aircraft Flight is immediately after an Act of Aircraft Takeoff (although real-world takeoffs include the initial climb of an aircraft to some altitude).

The Event Ontology defines an Act as "A Process in which at least one Agent plays a causative role." We will discuss agency later. Many human-centric Acts are considered in the CCO to be Planned Acts, "An Act in which at least one Agent plats a causative role and which is prescribed by some Directive Information Content Entity held by at least one of the Agents." Information Content Entities (ICEs) are just that, entities which are collections of some definite information, like a PDF, a word document, the Constitution. An ICE is not just the words, the ink on the paper, the bytes of the file, but the semantic meaning of the information. We will learn more about ICEs shortly.

Many processes in the Event Ontology are not Acts of Planned Acts, like Mechanical Processes, Natural Processes (Birth, Death), or Motion—motion is different from an Act of Motion, which involved an Agent, and does not refer to the physics involved, like Motion does.

What kinds of things are involved in Ice Cream Production? On your own, think about it for a moment, and then continue with the next paragraph.

The overarching act might be an Act of Manufacturing. There are many parts of the process of producing ice cream, and BFO-CCO allows processes to be parts of other processes; the CCO has a relation 'has process part.' Act of Manufacturing itself is a subclass of 'Act of Artifact Processing.' Let's take a detour through the Artifact Ontology to find out what this means.

An Artifact is a "Material Entity that was designed by some Agent to realize a certain function." A spoon is a great example, in our ice cream context: designed by some manufacturer to realize the function of Food Manipulation, like other cutlery. Brakes on a car realize the function of slowing and bringing a car to a stop. Basic Formal Ontology defines a function, roughly speaking, as the reason something exists, which depends on its physical make-up: average clothes bear a protective function, designer clothes bear an aesthetic function—there are different reasons why they exist. A ventilator, for example, clearly has just one function, but parts of it may have other functions, like a display screen that gives updates on how efficiently the ventilator is working. Cars bear one function, but the stereo system bears another, and the rear-view mirror bears another, and so on.

Some artifacts are specifically designed to bear information, like database servers or printer-paper, which are 'Information Bearing Artifacts.' Technically, _empty_ notebooks are 'Information Medium Artifacts' which become 'Information Bearing Artifacts' when information is recorded in them.

All of the machines in our ice cream plant play a specific 'role' in the process (BFO uses role differently, as we will see)—they were all built with some specific function in mind. A Freezer bears a Freezing Function, which we may define as "An Artifact Function that is realized in a process of lowering temperature below 32 degrees Fahrenheit." We could have said also "An Artifact Function that is realized in an Act of Freezing," and defined Act of Freezing as "An Act in which some Artifact lowers the temperature of some site, material entity, or spatial region below 32 degrees Fahrenheit."

For the purposes of this tutorial, we are going to suppose that there are three machines in our production process, a mixer, the Mix-o-Max 1000, the churner, the Churn-Plex, and the freezer, the Freez-o-Flash. Can you create these instances in our ontology as instances of the class Material Artifact? From there, can you create the classes freezing, mixing, and churning functions, and assert that those instances of machines 'bear' instances of those three functions? The graph looks like this:

![](RackMultipart20231023-1-yxeifw_html_b24558a9e4a83f61.png)

Our full graph will look like this:

![](RackMultipart20231023-1-yxeifw_html_a7b9aef1b926787a.png)

What about the people who work in the plant? Didn't we say that Planned Acts, like mixing and Freezing, involved Agents? Yes.

**Object Properties**

'Participates in' is the most generic relation that entities can have with processes. I participate in the Act of Walking; my shoes participate in that same Act of Walking, and so on. 'Agent in' is the relation that describes what material entity is the agent in that process; it has some causative weight to it. I am certainly the agent in the Act of Walking, but if I'm a passenger in a moving car, I am only a participant in an Act of Vehicle Use, the driver is the agent in that case. The agent in a process may be unknown, and the agent relation aims to capture agency when it is necessary to model the agent in some process.

Process, manufacturing and material processing processes particularly, require inputs and yield outputs. Milk 'is input of' an Act of Manufacturing, which has as its output ice cream. There may be many different steps in the Act of Ice Cream Production, and we can model this if the data has the level of granularity that describes those different acts. If the data of an ice cream plant merely has the inputs and outputs, it may be unwise to model every step of the ice cream production process. Suppose, for example, an ice cream producer _does_ have careful descriptions and data about the various steps of their production process; in that case, it would be acceptable to model the steps.

In our ice cream ontology, a worker has the 'agent in' relation to those acts, depending on which worker is handling which machine.

The entire Act of Ice Cream Production occurs according to a series of steps laid out in a recipe for the ice cream, user manuals for the various machines, and performed by workers in the plant. We may use the 'uses' relation to assert that Perry's, the overall manufacturer, 'uses' a 'Vanilla Almond Recipe Information Content Entity' in the Act of Ice Cream Production. Perry's does not use this recipe in every act of production, but only those which have Vanilla Almond as an output.

The relation of 'uses' is like an instrumental relation, and it holds between agents and material entities. Perry's uses various machines in the Act of Manufacturing. We may want to model what machines are used in particular parts of the process, and we can assert that a worker uses a freezer in the Act of Freezing. This worker needs to be the 'agent in' this process.

The graph looks like this:

![](RackMultipart20231023-1-yxeifw_html_e3a1f0954cf02ed.png)

There's something slightly wrong with how we have been talking about the worker so far. The person who is manning the machine is not called 'worker,' they have a name, and they are in instance of a cco:Person, not an instance of a worker. A person becomes a worker by bearing a 'worker role.' We usually want to be more specific, so for our example, we should say that an our person John Smith bears an Ice Cream Worker Role, which distinguishes him from other more generic roles, and even other ice cream roles, like Ice Cream Servers.

**Roles**

Roles are in the same family as functions—all 'realizable entities.' Functions rely on the physical make-up of the entities that bear them, but roles do not. Roles are more social, extrinsically, rather than intrinsically grounded. Roles are given to people by Acts, by documents, organizations, or people. A person becomes a lawyer because the State Bar, a cco:Organizaton, recognizes them as a person who has the ability to practice law because of some criteria they fulfilled—namely, attending a law school and successfully passing the Bar Exam. A worker at an ice cream plant may have been hired by just one person, and that person may have created a document which explicitly declares that John Smith is hereby allowed to bear the role of Ice Cream Worker in this particular plant.

A common key design pattern used when discussing social responsibilities and roles is that a person or organization participate in some Act which produces a document (an ICE) that specifies some role, who can bear it, and how that role must be born. Take our lawyer, the State Bar Association got together in a committee meeting (Act) and produced a document (a certificate, an ICE) which declares that some person can be a lawyer (bear a lawyer role), and the rules they must follow to be allowed to keep bearing that role (not defrauding clients, for example).

![](RackMultipart20231023-1-yxeifw_html_9f3db6af6dc91973.png)

In this graph, Jack bears the role of 'Hiring Manager,' which was given to him at some point earlier by the company, or someone in the company with the ability to do that, and he is the 'agent in' an Act of Deliberation, which produces a document, that specifies a certain role.

2

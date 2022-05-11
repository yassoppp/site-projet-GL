---
title: Vocabulaire Anglais pour le Projet GL
---

{{< toc >}}

## Software Engineering

| French                                    | English                                                       | Definition/Comments                                                                                                                                                                                   |
| ---                                       | ---                                                           | ---                                                                                                                                                                                                   |
| Génie Logiciel                            | Software Engineering                                          | The art of making good software with limited ressources                                                                                                                                               |
| Maître d'œuvre                            | Project coordinator (or Project manager, or Project overseer) | The person or company in charge of carrying out a project (usually, the software provider)                                                                                                            |
| Maître d'ouvrage/Maîtrise d'ouvrage       | Works owner/Contracting owner                                 | The person or company which requested the project (usually, the client)                                                                                                                               |
| Cas de test                               | Test case                                                     | Elementary "thing" to try the program on.                                                                                                                                                             |
| Suite de tests                            | Test suite (or Test bench)                                    | Set of test cases.                                                                                                                                                                                    |
| Test unitaire                             | Unit test (test-case), Unit testing (activity)                | Test targeting a precise part of the software.                                                                                                                                                        |
| Test d'intégration                        | Integration test                                              | Test stressing several parts of the program under test. Usually done after individual parts have been successfully unit-tested.                                                                       |
| Test boite blanche (ou test structurels)  | White box test (aka clear box test, or structural test)       | Test case written with the internal details of the program in mind.                                                                                                                                   |
| Test boite noire (ou Test fonctionnel)    | Black-box test (or Functional test)                           | Test written without the knowledge about the internals of the software.                                                                                                                               |
| Test d'acceptation                        | Acceptance test                                               | Set of test cases that must pass before a release.                                                                                                                                                    |
| Développement dirigé par le test          | Test-driven development                                       | Development methodology consisting in writing test-cases before writing the actual source code.                                                                                                       |
| Gestionnaire de version                   | Version control system (or Revision control system)           | Software allowing people to work together on a project while archiving all of the old versions.                                                                                                       |
| Gestionnaire de bugs                      | Bug tracker                                                   | Database of known present and past bugs of a program.                                                                                                                                                 |
| Gestion qualité                           | Quality management                                            | Set of techniques for ensuring that all the activities necessary to design, develop and implement a product or service are effective and efficient with respect to the system and its performance.    |
| Assurance qualité                         | Quality assurance (QA)                                        | Systematic application of quality management methods.                                                                                                                                                 |
| Planning prévisionnel                     | Provisional schedule                                          | Expected schedule for a project.                                                                                                                                                                      |
| Planning effectif                         | Actual schedule                                               | How the project actually took place.                                                                                                                                                                  |


## Compilation

| French                                                                                    | English                                                   | Definition/Comments                                                                                                                               |
| ---                                                                                       | ---                                                       | ---                                                                                                                                               |
| Lexicographie                                                                             | Lexicography                                              | Analysis of a program at the "word" level.                                                                                                        |
| Lexème                                                                                    | Token                                                     | atomic group of characters produced by the lexical analysis.                                                                                      |
| Un automate, des automates                                                                | An automaton, several automata                            | State-machine                                                                                                                                     |
| Analyse syntaxique                                                                        | Syntax analysis (or Parsing)                              | Analysis of complete program constructs.                                                                                                          |
| Grammaire hors-context                                                                    | Context-free grammar                                      | Set of production rules in which the left hand side consist of only one non-terminal symbol.                                                      |
| Grammaire sous-context                                                                    | Context-sensitive grammar                                 | Set of production rules in which the left hand side and the right hand side may be surrounded by a context of terminal and non-terminal symbols.  |
| Typage (ou Analyse sémantique (statique))                                                 | Typing, type-checking (or (Static) semantic analysis)     | Checking that a program is well-typed.                                                                                                            |
| Génération de code                                                                        | Code generation                                           |                                                                                                                                                   |
| Arbre de syntaxe abstraite (ou Arbre syntaxique asbtrait, ou simplement Arbre abstrait)   | Abstract Syntax Tree (AST)                                | Tree structure representing the parsed program.                                                                                                   |
| Grammaire attribuée                                                                       | Attribute grammar                                         | A formal way of denoting contextual aspects of a language.                                                                                        |
| Table à adressage dispersé (ou Table de "hachage")                                        | Hash table                                                | An efficient dictionary structure.                                                                                                                |
| Compilateur                                                                               | Compiler                                                  | Program transforming source code into assembly language.                                                                                          |
| Assembleur                                                                                | Assembler                                                 | Program transforming assembly code into machine executable code.                                                                                  |
| Éditeur de liens                                                                          | Linker                                                    | Program assembling several pieces of binary code together.                                                                                        |
| Langage d'assemblage                                                                      | Assembly language                                         | Human-readable form of the machine code.                                                                                                          |
| Système de compilation                                                                    | Build system                                              | System in charge of calling the compiler(s), linker, ... on the right files with the right options.                                               |


## Java, Object Oriented Programming

| French                                                | English                                       | Definition/Comments                                                       |
| ---                                                   | ---                                           | ---                                                                       |
| Classe                                                | Class                                         | Type of an object.                                                        |
| Objet                                                 | Object                                        | Instance of a class.                                                      |
| Champ (ou attribut, ou variable membre)               | Field (or data member)                        |                                                                           |
| Méthode (ou fonction membre)                          | method (or member function)                   |                                                                           |
| Héritage                                              | Inheritance                                   | Way to define a class based on its base class.                            |
| Classe mère (ou Classe de base)                       | Base class (or Parent class, Super-class)     | Class from which another class derives.                                   |
| Classe fille (ou Classe dérivée)                      | Derived class (or Subclass, or Child class)   | Class deriving from another.                                              |
| Surcharge de méthode                                  | Method overloading                            | Defining different methods with the same name and different signatures.   |
| Redéfinition de méthode                               | Method redefining                             | Redefining a method with the same signature in a subclass.                |
| Résolution dynamique de méthode (ou Liaison tardive)  | Dynamic binding (or Late binding)             | Calling a method based on the run-time type of the object.                |
| Affectation                                           | Assignment                                    | Operation providing a new value to a variable.                            |


## School

| French                | English               | Definition/Comments                                                           |
| ---                   | ---                   | ---                                                                           |
| Cours d'Amphi         | Lecture               | Class with all students                                                       |
| Travaux dirigés       | Tutorial              | Class with small groups of students                                           |
| Travaux pratiques     | Lab works             | Practical experimentations                                                    |
| Séance de suivis      | Progress meeting (?)  | Meetings during which the students explain their progress with the project.   |
| Soutenance            | Defense               | Presentation by students                                                      |


## False Friends

| French                        | English                   | Definition/Comments                                                                                                                                                           |
| ---                           | ---                       | ---                                                                                                                                                                           |
| Finalement                    | Eventually                | At the end                                                                                                                                                                    |
| Enfin                         | Finally                   | At last                                                                                                                                                                       |
| Réaliser un projet            | To carry out a project    |                                                                                                                                                                               |
| Réaliser, se rendre compte    | To realize                |                                                                                                                                                                               |
| Être affecté, être touché     | Affectation               | An attempt to assume or exhibit what is not natural or real; false pretense; artificial appearance, or show; as, an affectation of wit, or of virtue (Webster's dictionary)   |
| Actuel                        | Current                   | The one as of now                                                                                                                                                             |
| Réel                          | Actual                    | Real, concrete.                                                                                                                                                               |
| Plan d'un exposé              | Outline of a talk         |                                                                                                                                                                               |
| Plans pour l'avenir, projets  | Plans                     |                                                                                                                                                                               |

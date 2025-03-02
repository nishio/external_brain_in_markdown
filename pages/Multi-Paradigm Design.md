
[[James O. Coplien]] July 8, 2000 11:58 am [PDF](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.84.7630&rep=rep1&type=pdf)

Paradigm p.17
- > We use these foundations of commonality and variation to formalize the concept of paradigm. A paradigm, as the term is popularly used in contemporary software design, is a way of organizing system abstractions around properties of common- ality and variation. The object paradigm organizes systems around abstractions based on commonality in structure and behavior and variation in structure and algorithm. The template paradigm is based on structural commonality across family members, with variations explicitly factored out into template parameters. Overloaded functions form families whose members share the same name and semantics, and in which each family member is differentiated by its formal param- eter types.
    - なるほどね。C++にはオブジェクト指向以外にもテンプレートや関数オーバーロードという手段がある、これは明らかにオブジェクト指向の手段ではない、強いC++erはこのそれぞれの手段を使い分けるが、一体どういう時にどれを使うのが良いのか？という話らしい

1.3.4 Domains p.33
- > A domain is an area of specialization or interest. We talk about the application domain—the body of knowledge that is of interest to users. Because it is of interest to users, it is hopefully of interest to us. We break down application domains into application subdomains—we divide and conquer. We talk about the solution domain, which is of central interest to the implementors but of only superficial interest to system users. Any given design may deal with multiple solution domains at once, for example, C++ constructs, patterns, and maybe state machines and parser-generators.
    - アプリケーションドメインはユーザが関心を持つものに対しての知識の集まり
    - ソリューションドメインは実装する人が関心を持つものに対しての知識の集まり

- Chapter 2 Commonality Analysis p.55
    - 2.1 Commonality: The Essence of Abstraction
        - 2.1.1 Deductive and Inductive Commonality
        - 2.1.2 Software Families
            - Finding Domains
    - 2.2 Priming Analysis: The Domain Vocabulary
        - 2.2.1 The Domain Dictionary
        - 2.2.2 Design Epistemology
    - 2.3 Dimensions of Commonality and Commonality Categories p.64
        - 2.3.1 (Data) Structure
        - 2.3.2 Name and Behavior
        - 2.3.3 Algorithm p.75
    - 2.4 Examples of Commonality
    - 2.5 Reviewing the Commonality Analysis
    - 2.6 Commonality and Evolution
- Chapter 3 Variability Analysis p.85
    - 3.1 Variability: The Spice of Life
    - 3.2 The Commonality Base
    - 3.3 Positive and Negative Variability
        - 3.3.1 Positive Variability
        - 3.3.2 Negative Variability
    - 3.4 The Domain and Range of Variability
        - 3.4.1 The Text Editing Buffers Example
        - 3.4.2 Good Parameters of Variation
    - 3.5 Binding Time
        - 3.5.1 Binding Time and Flexibility
        - 3.5.2 Are Objects about Deferred Binding?
        - 3.5.3 Efficiency and Binding Time
        - 3.5.4 Binding Time Alternatives p.93
            - Source Time
            - Compile Time
            - Link (and Load) Time
            - Run Time
    - 3.6 Defaults
    - 3.7 Variability Tables p.95
    - 3.8 Some Variability Traps
    - 3.9 Reviewing the Variability Analysis
    - 3.10 Variability Dependency Graphs
- Chapter 4 Application Domain Analysis
    - 4.1 Analysis, Domain Analysis, and Beyond
        - 4.1.1 Traditional Analysis
        - 4.1.2 System Families: Domain Analysis
            - Family Members in the Application and Solution Domains
            - Balancing Abstraction and Specification
            - Levels of Domain Abstraction p.105
        - 4.1.3 Application Domain Analysis and Solution Domain Analysis
        - 4.1.4 The Activities of Domain Analysis
    - 4.2 Subdomains within a Domain Analysis
        - 4.2.1 Domain Analysis and Reuse
        - 4.2.2 Subdomain Modularity
        - 4.2.3 Iteration and Hierarchy
    - 4.3 The Structure of a Subdomain p.114
        - 4.3.1 Frameworks as Subdomain Implementations
        - 4.3.2 The Activities of Subdomain Analysis
    - 4.4 Analysis: The Big Picture
- Chapter 5 Object-Oriented Analysis
    - 5.1 About Paradigms and Objects
        - 5.1.1 Classes and Objects
        - 5.1.2 Liskov Substitutability Principle
        - 5.1.3 Virtual Functions
        - 5.1.4 Object Orientation: Yet Another Definition
            - Positive versus Negative Variability
            - Binding Time
            - Defaults
        - 5.1.5 The Suitability of Object-Oriented Design
            - Language and Paradigm
    - 5.2 Object-Oriented Commonality Analysis
        - 5.2.1 Commonality Analysis
        - 5.2.2 Variability Analysis
- Chapter 6 Solution Domain Analysis
    - 6.1 The “Other” Domain
        - 6.1.1 Analysis and Language
    - 6.2 The C++ Solution Domain: An Overview
:
| Data  | a mechanism to group families of related values |
| -- | -- |
| Overloading | a mechanism to group families of related functions |
| Templates | which group related algorithms or gross data structures |
| Inheritance | which groups classes that behave the same *** |
| * | which also groups classes that behave the same but with later binding than inheritance alone provides |
| **  | typically used for fine-grain variations in code and data |
        - *: Inheritance with virtual functions
        - **: Preprocessor constructs, such as `#ifdef`
        - ***:  (usually public inheritance; we treat private inheritance separately in Section 6.11)
    - 6.3 Data
    - 6.4 Overloading
        - a mechanism to group families of related functions
    - 6.5 Class Templates
        - 6.5.1 Template Specialization
    - 6.6 Function Templates
    - 6.7 Inheritance
        - 6.7.1 Aligning Domains
    - 6.8 Virtual Functions
    - 6.9 Commonality Analysis and Polymorphism
    - 6.10 Preprocessor Directives
    - 6.11 Negative Variability
        - 6.11.1 Deciding When to Use Negative Variability
            - A Template Example
            - An Example of Argument Defaulting
            - An Example of Data Cancellation
            - An Example of Behavior Cancellation
            - An Example of Contravariance
            - An Example of `#ifdef`
        - 6.11.2 Negative Variability versus Domain Splitting
            - An Example of Behavior Cancellation
            - A Template Example
            - An Example of Data Cancellation
            - An Example of `#ifdef`
        - 6.11.3 A Summary of Negative Variability
    - 6.12 Extended Solution Domain Constructs
        - 6.12.1 Multiple Inheritance
            - First case: Multiple Domains
            - Second case: Mix-ins
        - 6.12.2 Design Patterns
            - Patterns Beyond Language
            - Patterns and Multi-Paradigm Design
            - Aliases for Solution Domain Constructs
            - Higher-Level Than Programming Language Constructs
            - Negative Variability
            - Multi-Paradigm Tools as a Patterns Adjunct
    - 6.13 A Summary of the C++ Solution Domain: A Family Table
    - 6.14 Relative Power of Paradigms
- Chapter 7 Simple Mixing of Paradigms
    - 7.1 Putting It All Together: An Overview of Multi-Paradigm Design
        - 7.1.1 One Size Does Not Fit All
        - 7.1.2 Degrees of Complexity
            - Single Domain, Single Paradigm
            - Multiple Decoupled Subdomains, Single Paradigm
            - Multiple Decoupled Subdomains, Single Paradigm for Each Subdomain
            - Multiple Decoupled Subdomains, Multiple Paradigms for Each Subdomain
            - Multiple Subdomains in a Directed Acyclic Graph (DAG), Multiple Paradigms
            - Circular Subdomains
        - 7.2 Activities of Multi-Paradigm Design
            1. Divide the problem into intuitive subdomains (Section 4.1.4).
            2. Has this been done before?
            3. Analyze each application subdomain (Chapter 4).
            4. Analyze the solution domains (Chapter 6).
            5. Map from application domain analysis onto available solution domain anal- yses (Chapter 7).
            6. Evaluate opportunities for Application-Oriented Languages (AOLs).
        - 7.3 Example: A Simple Language Translator
            - 7.3.1 Partitioning the Domain into Subdomains
                - Choosing a Partitioning
                - Domain Analysis
                - The “Glue” Domain
                - Domain Analysis and Iteration
            - 7.3.2 Finding the Right Paradigms within a Subdomain
                - The Domain Vocabulary
                - Commonality Analysis of the Domain
                - Returning to the Question of Line Numbers and Labels
        - 7.4 Design, Not Analysis
            - 7.4.1 Analysis, Architecture, or Design?
            - 7.5 Another Example: Automatic Differentiation
                - 7.5.1 Basic Operations Domain
                - 7.5.2 Degree Domain
                - 7.5.3 Value Domain
                - 7.5.4 Evolving the Design
            - 7.6 Outboard Paradigms
            - 7.7 Management Issues
                - 7.7.1 Occam’s Razor: Keeping Things Simple

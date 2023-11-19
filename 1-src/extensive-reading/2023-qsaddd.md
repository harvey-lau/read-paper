# The Extensive Reading of 2023-[*A Qualitative Study on the Implementation Design Decisions of Developers*](https://dl.acm.org/doi/10.1109/ICSE48619.2023.00047)

- The **problem** is that "while prior work has studied developer decision-making, the choices made while choosing what solution to write in code remain understudied".
- The **solution** is a mixed-methods study, examining the phenomenon where developers select one specific way in many potential alternatives to implement a behavior in code (implementation design decisions).

For example, how should I represent my matrix data—Python arrays, C++ arrays, or third-party libraries?

If the developer wanted to minimize runtime, they could use C++ arrays or third-party libraries. If they wanted a simple, easy-to-read solution for their teammates, they could opt for Python arrays.

This study includes 46 surveys responses and 14 semi-structured interviews with professional developers about their decision types, considerations, processes, and expertise for implementation design decisions.

**RQ1**-What implementation design decisions do software developers make? See Table 2.

- Alternatives—Deciding what high-level approaches to use to address a particular problem.
- **Behaviors**—Deciding the program specification: what parameters to set for a program and their types, what outputs the program should give, and the behavior of the program.
- Data—Deciding how to manage data within software: what data should be handled in a program, how it should be represented, and how it should be interacted with.
- **Code constructs**—Deciding which programming language constructs to use within a program.
- Structure—Deciding how to organize the codebase, where files should lie, and how code should be modularized.
- Programming languages, APIs, services—Deciding the programming languages, APIs, or third-party services to use in the software system or script.
- Automation—Deciding whether to implement a technology solution from scratch.
- Reuse—Deciding whether code should be reused and to what extent it should be general enough to be extended to different scenarios.
- **Updates**—Deciding whether to update the software or not.

**RQ2**-What considerations do software developers have while making implementation design decisions? See Table 3.

- **Community Support**—How well-supported by a developer community a technology is.
- Features—The features a technology contains.
- Popularity—The number of users that use the technology or library.
- Reliability—How reliable and correct the software is.
- Security—How secure software is; robustness of software to adversarial attacks.
- Maintainability—How easily maintenance actions (e.g., fixing defects, updating components) can be performed on software.
- Testability—How easily software can be tested (e.g., unit tests).
- Extensibility—How easily the code can be extended to accommodate changes (e.g., new features).
- Performance—Performance aspects of the code (e.g., runtime, memory).
- Reproducibility—Whether code is able to reproduce the same output, given the same input.
- Requirements—The requirements of the software; customer needs.
- **Future Requirements**—Requirements or customer needs that may or may not occur in the future.
- Skills—The current skills of the team or of the developer.
- Budget—Amount of resources (e.g., time, money) available to implement the software project.
- Reusing Resources—Reusing existing resources (e.g., code, practices).
- Difficulty—How much effort completing the implementation will be.
- Readability—How easily code syntax is read by a developer.
- Code Cleanliness—The quality of the implementation’s code; how easy it is to onboard other developers and make updates.
- Simplicity–The length or complexity of the implementation.
- **Consistency**—Being consistent with the code style of the programming language or code base.
- **System Fit**—How well the implementation fits in with an existing code base or system.
- Data—How data in the system will be managed or handled.
- Impacts—The impacts that the implementation may cause.
- Users—Thinking about collaborators who will be working in the code base; the usability of the software for end-users.
- Documentation—Writing documentation for the implementation.

**RQ3**-What process do software developers follow to make implementation design decisions? See Table 4 and Table 5.

The types of actions developers take while making implementation design decisions:

- Defining Problem Space
  - Providing Context—Explaining context about the problem the developer is facing (e.g., refactoring).
  - Defining Requirements—Defining the requirements of the solution, considering user needs, business needs, and organization needs.
  - **Updating Requirements**—Updating the requirements of the solution after they are initially defined.
- Ideating
  - Brainstorming—Brainstorming potential solutions that could solve the problem.
- Assessing
  - **Evaluating**—Evaluating the developer’s current situation; considering the pros and cons for each solution.
  - Estimating—Estimating the potential costs associated with implementation.
- Prototyping
  - **Proof-of-Concept**—Building a proof-of-concept for a potential solution.
- Implementing
  - Choosing—Choosing a solution to implement.
  - Planning—Planning the steps needed to implement the solution.
  - Implementing—Implementing a particular solution.
  - Updating Implementation—Trying a new implementation or updating an existing one based on previous implementation attempts.
  - Deploying—Releasing the solution to the public.
- Verifying
  - Reviewing—Having others review and provide feedback to the solution.
  - Testing—Testing the implementation for functionality and potential defects.
- Updating Knowledge
  - **Researching**—Learning more about the problem or potential solutions.

The sequence of actions that developers follow:

1. Providing Context
2. Researching
3. Defining Requirements
4. Brainstorming
5. Estimating
6. Evaluating
7. Choosing
8. Planning
9. Proof-of-Concept
10. Updating Requirements
11. Implementing
12. Reviewing
13. Testing
14. Updating Implementation
15. Deploying

**RQ4**-Which types of developer expertise are described in the implementation design decision-making process? See Table 6.

- Decision Making
  - Knowledgeable about customers and business
  - Sees the forest and the trees
  - Knowledgeable about tools and building materials
  - Knowledgeable about their technical domain
  - Knowledgeable about engineering processes
  - Models states and outcomes
  - Handles complexity
  - Knowledgeable about people and the organization
  - Updates their mental models
- Software & Designs
  - Carefully constructed
  - Fitted
  - Evolving
  - Attentive to details
  - Anticipates needs
  - Creative
  - Long-termed
  - Elegant

# The Extensive Reading of 2023-[*AI-based Question Answering Assistance for Analyzing Natural-language Requirements*](https://www.computer.org/csdl/proceedings-article/icse/2023/570100b277/1OM4xJrN14Y)

- The **problem** is that some processes about requirements, when carried out entirely manually, are tedious and may further overlook important quality issues due to time and budget pressures.
- The **solution** is QAssist, a question-answering (QA) approach that provides automated assistance to stakeholders, including requirements engineers, during the analysis of NL requirements.

Figure 1 shows a good example for introducing the application scenarios of QAssist.

The workflow of QAssist (refer to Figure 2 for more details) is:

QAssist takes as **input** a question ($q$) posed in NL by the user and a software requirements specification (SRS).

1. **Document Retriever**: QAssist retrieves the most relevant document ($d$) to $q$ from an external domain-specific corpus ($D$).
2. **Splitting**: QAssist generates a list of text passages ($T$) by splitting the input SRS and $d$.
3. **Passage Retrieval**: QAssist then finds the top-$k$ text passages ($R \subset T$) that are most relevant to $q$.
4. **Answer Extraction**: QAssist extracts a likely answer from each text passage.

QAssist finally returns as **output** the relevant text passages from step 3 alongside the answers extracted in step 4.

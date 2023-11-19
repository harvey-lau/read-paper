# The Extensive Reading of 2023-[*APICad: Augmenting API Misuse Detection through Specifications from Code and Documents*](https://ieeexplore.ieee.org/document/10172771)

- The **problem** is that current tools providing the specifications of API either depend on the quality of the code or are limited to the irregularity of the documents.
- The **solution** is APICad, to detect API misuse bugs of C/C++ by combining the specifications mined from code and documents.

APICad has 4 modules (refer to Figure 1 for its workflow):

1. **Encoded context building** module aims to infer the usage semantics from the context of API invocations, which can be used to mine specifications and serve as target objects for detection.
   1. To save cost and ensure effectiveness, APICad performs under-constrained symbolic execution to selectively explore paths for generating feasible traces to each API call site.
   2. The usage semantics of the traces are extracted and dumped into feature vectors to represent encoded contexts.
2. In **frequency-based specification mining** module, APICad statistically mines 3 types of API specifications based on the frequency of the corresponding features in the encoded contexts of an API.
3. **Specification construction from documents** module is in parallel with the above 2 modules for analyzing documents. It will classify the sentences of API documents to different usage types through the corresponding keyword-based templates. Furthermore, the techniques in NLP are leveraged to capture the semantics carried by the classified sentences for constructing the API specifications.
4. **Bug detection with combined specification** module combines the specifications from code and documents by logical disjunction and the union operation. To a given target API, it judges whether there are bugs among them with the combined specifications.

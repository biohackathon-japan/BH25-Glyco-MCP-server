---
title: 'DBCLS BioHackathon 2025 report: Natural Language to SPARQL Workflows for Glyco Data Integration using GlyCosmos and PubChem APIs via an MCP Server'
title_short: 'BioHackJP25: Natural Language Queries to GlyCosmos & PubChem'
tags:
  - Semantic web
  - SPARQL
  - API
  - Ontologies
  - Workflows
  - MCP
  - LLM
authors:
  - name: Miguel Mazumder
    orcid: 0000-0003-1181-8118
    affiliation: 5
  - name: Akira R. Kinjo
    orcid: 0000-0002-4006-8208
    affiliation: 1
  - name: Yasunori Yamamoto
    orcid: 0000-0002-6943-6887
    affiliation: 2
  - name: Issaku Yamada
    orcid: 0000-0001-9504-189X
    affiliation: 3
  - name: Masae Hosoda
    orcid: 0000-0002-4750-4041
    affiliation: 2
  - name: Priscilla Joanne
    affiliation: 4 

affiliations:
  - name: Anima Machina, G.K.
    index: 1
  - name: Database Center for Life Science, ROIS-DS
    index: 2
  - name: The Noguchi Institute
    index: 3
  - name: The University of Tokyo
    ror: 057zh3y96
    index: 4
  - name: The Noguchi Institute
    index: 5

date: 19 September 2025
cito-bibliography: paper.bib
event: BH25JP
biohackathon_name: "DBCLS BioHackathon 2025"
biohackathon_url: "https://2025.biohackathon.org/"
biohackathon_location: "Mie, Japan, 2025"
group: Glyco MCP Server
git_url: "https://github.com/biohackathon-japan/BH25-Glyco-MCP-server"
authors_short: "Mazumder M., Priscilla J. \\emph{et al.}"
---

# Introduction

As part of the DBCLS BioHackathon 2025, we are here to report on behalf on the Glyco MCP server project team. The aim of this project is to investigate how MCPs (Model Context Protocols) can be applied to facilitate the research query process between GlyCosmos and PubChem. By integrating glycan-related data (structures, synthesis genes, glycoprotiens, and glycolipids) through extensive SPARQList resources, we aim to enable natural language access to these datasets. This approach lowers the barrier for researchers unfamiliar with SPARQL or RDF, while supporting reproducible and modular workflows.

# Background

While GlyCosmos provides rich programmatic access to glycans, genes, glycoprotiens and related information through SPAQRL queries and SPARQList endpoints, practical use of this access requires detailed knowledge of their parameters, query syntax, and JSON outputs. Similarity, while PubCHem offers chemical identifies and structures through its own APIs, integrating these with glycoinformatics resources requries writing multi-step federated queries in SPARQL or custom scripts. For many researchers with biology or chemistry background, this can appear as a steep learning curve with high risk of fragile workflows. For example, GlyCosmos currently organizes data across more than 150 RDF graphs, each of which may need to be addressed differently depending on the query, or point to specific information that a researcher may not be aware exists in that graph.

As a result, users will often default to manual browsing of GlyCosmos or GlyTouCan web portals. While these interfaces are valauable for preliminary explorartoy serachers, they have little flexibility when researchers need to perform specific actions such as :
- chain multiple queries (e.g disease -> gene -> glycan -> PubChem ID)
- retreive structued outputs as scale
- apply the same query across multiple different IDs

To address this gap between glyco researchers and complex retrieval of information from Glycosmos, we intend of implementing a mapping of natural language questions to existing GlyCosmos SPARQList APIs. This will allow researchers to ask questions such as species to glycan association, WURCS and GlycoCT sequences for a Glytoucan ID, or Disease to glycan association and retrive associated PubChem compounds. Instead of manually browisng or construction of SPARQL queries, these questions are automatically resolved into API calls with the approriate parameters. This approach offers a more inuitive and simple form of access to Glycosmos and PubChem.

Our work demonstrates how MCP servers can serve as a middleware layer than translates researcher-freindly natural language queries into SPARQL queries via SPARQList endpoints, enabling for a more robust integration acrses GlyCosmos and PubChem resources.

# Methodology
Our team approached this project as relative newcomers to Model Context Protocols (MCPs), SPARQL queries, RDF data integration, and GlyCosmos as well. With very limited prior experience in these areas, our first step was to explore the existing GlyCosmos SPARQL queries PIs in order to understand what is expected for this natural langauge to SPARQL queries process.

We began by defining a set of use cases that would be feasible for mapping natural language queries to SPARQL endpoints. This required some background knowledge of glycans, biology, and the organization of GlyCosmos and PubChem resources. Initially, we experimented with complex chain queries targeted at specific biological questions (e.g., disease -> gene -> glycan -> PubChem compound). In this phase, our collaborators from PubChem contributed by sharing federated query examples to map to the natural language question use cases we determined were relevant for researchers.

While promising in principle, this approach quickly revealed several limitations. Current large language models and tooling are not yet reliable for generating consistent accurate SPARQL syntax [@discusses:citesAsEvidence:Pan2025FIRESPARQL], and the structure of GlyCosmos itself spread across more than 150 RDF graphs. With this approach of mapping complex chained federated queries directly to natural language, large language models would only be capable of reproducing queries within the same narrow scope, severely limiting their ability to create a comprehensive training dataset.

Consequently, we decided to turn to the GlyCosmos SPARQLlist API endpoints as an alternative. The advantage of using these endpoints is that they provide modular, predefined queries that act as atomic building blocks. By creating natural language mappings for each atomic query, we would create a consistent way to translate natural language questions into API calls. Once these atomic mappings were defined, they could be combined into chain mappings, allowing us to construct more complex workflows as we documeneted more releveant predefined queries. In this way, atomic YAML mappings serve as the foundation for constructing chained workflows, a process illustrated in Figure 1.

So in parallel we also tested the GlyCosmos SPARQList APIs to determine the predefined SPARQL queries available for mapping. During this exploration, we discoverd an major issue. THere are a total of 373 SPARQList API endpoints, and only 89 are available for mapping. Of the non-functional APIs, 43 sparqlist queries reference outdated graphs and 246 of the apis return address errors are are unusable. Consequently, our work focused only on the subset of APIS that could return valid data.

To support LLM-based mapping of natural language queries, we designed a structured YAML schema. The schema included metadata describing its purpose, general rules for how SPARQList APIs should be called, and detailed API specifications (endpoint, required parameters, output fields, and descriptions). We also provided a set of natural language use cases paired with their corresponding API mappings, which functioned as few-shot examples for the LLM. These elements together enabled the LLM to interpret user queries in context and reliably produce valid API calls. The use cases and api endpoint descriptions remain in the same file to ensure consistency during documentaiton and updating of this process.

Need to add section of how the actual llm and mcp server operate

# Results

## MCP Server testing
We implemented a YAML-based mapping of natural language questions to GlyCosmos SPARQList API endpoints, starting with atomic queries. Using these atomic mappings as few-shot training examples, we demonstrated that large language models (LLMs) could correctly interpret natural language inputs and resolve them into valid API calls.

Testing with the Claude LLM integrated through the MCP server showed that the system was able to perform atomic queries reliably. For example, questions such as “What is the amino acid sequence of UniProt protein P02873?” or “Show me the glycan image for GlyTouCan ID G00051MO” were successfully translated into the correct API calls, with structured results returned.

We also evaluated chained workflows defined in the chaining YAML. With minimal prompting and guidance, Claude was able to execute multi-step queries such as:

“Find information about epitope EP0007, including its glycan image and external database links.”

1: Call Glyco Epitope (get GlyTouCan ID) with epitopeID=EP0007 → returns the corresponding GlyTouCan ID.

2: Call Get image data from GlyTouCan with the returned GlyTouCan ID → retrieves a glycan structure image in SNFG notation.

3: Call External ID from GlyTouCan with the same GlyTouCan ID → retrieves cross-references to external databases (KEGG, GlyGen, UniCarb-DB).

This confirmed that chaining atomic API calls is a feasible and robust alternative to constructing strictly structured federated SPARQL queries.

However, integration of PubChem queries directly into the MCP embeddings was not achieved during the hackathon timeframe. While PubChem collaborators provided federated query examples, we did not succeed in embedding these cross-source workflows with the atomic api descriptiopn and language mapping used by the LLM for Glycosmos API calls. As a result, our current workflows are restricted to GlyCosmos endpoints, with cross-database queries identified as a priority for future work.

## GLycosmos API Documentation
As part of our evaluation, we systematically tested all 373 GlyCosmos SPARQList API endpoints. Each endpoint was categorized into one of three states, Working (87 endpoints), Outdated query (43 endpoints) and Error (246 endpoints). This documentation provides both a snapshot of the current functionality of GlyCosmos APIs and a roadmap for maintenance. For our project, only the 81 working endpoints can currently be incorporated into the atomic YAML mappings. By explicitly recording endpoint status, we established a foundation of few-shot learning examples for LLMs and API maintenance and extension.
This audit not only supported our hackathon goals but also improving the broader GlyCosmos community, as future work can build upon this curated lists for imrpoved SPARQList endpoint maintenance and expansion

## Use case: Integration of Claude LLM with MCP Server for GlyCosmos
To evaluate the YAML mapping as a prompt, several types of natural language questions were prompted to Claude chat session connected to the MCP server. The prompt specifies the LLM to only use the provided API functions in the MCP server in order to exclude information the LLM might retrieve outside the API.

First question type is a rephrase of example use case in the YAML description that only requires one API call. As expected, the LLM can chose the intended API function. Secondly, Claude LLM was also asked a rephrase of example use case that requires a chain of API calls. The LLM can also correctly choose the correct test case and follows the instruction exactly and retrieve the correct information. Third, Claude LLM was tested with a more vague question. For example, "Give me all the information about EP0009". The exact kind of information to be searched and the type of ID was not explicitly provided. The LLM can successfully recognize the type of ID given and therefore use the appropriate API calls. It was also successful at chaining API calls that was not described in the YAML. The question "Give me all the information about EP0009" was followed with "how about to pubmed?". It tried to use get_pubchem_compound_id(), even though it was not explicitly told in the description it was for glycans. It tried querying "EP0009" at first and failed, then it tried querying the corresponding glycan "G78706CK", which returned a Pubchem compound ID. It was able to chain this result with another API call with compound ID as input to display various compound attributes pulled from Pubchem. The whole chat session of the evaluation can be accessed through this link: https://claude.ai/share/ececea39-6790-4809-92c2-525971333b0a.

# Discussion
One limitation is that the API only allows for one input at a time. For the example question "tell me about glycans that bind to influenza virus", there is actually 30 glycans that bind to the influenza virus recorded in GlyCosmos. Claude LLM then tried to query all the glycans one by one.

# Future Directions

Beyond programmatic integration, the project also explored outreach to experimental reserachers. Glycan projdcts used in laboratories while available from many companies, often have unclear information where a given glycan can be purcahsed. With integration of natural langauge questions to glycan purchase information could facilitate this process for researchers and scientists.

talk about documentaiton of working and outdated sparql api list, and continue adding to use case list

did not create atmoic queries for Pubchem but that will be to create natural language mapping to their PUG-REST and PubChemRDF REST endpoints.
...

## Acknowledgements

...

## References
references:
  - id: Pan2025FIRESPARQL
    title: "FIRESPARQL: A LLM-based Framework for SPARQL Query Generation over Scholarly Knowledge Graphs"
    authors:
      - name: Xueli Pan
      - name: Victor de Boer
      - name: Jacco van Ossenbruggen
    year: 2025
    publisher: arXiv
    journal: "Proceedings of the 17th International Joint Conference on Knowledge Discovery, Knowledge Engineering and Knowledge Management (IC3K)"
    doi: 10.48550/arXiv.2508.10467
    url: https://doi.org/10.48550/arXiv.2508.10467

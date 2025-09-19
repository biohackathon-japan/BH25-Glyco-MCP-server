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
  - name: First Author
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Second Author
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: Third Author
    orcid: 0000-0000-0000-0000
    affiliation: 1
  - name: Miguel Mazumder
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: NAME
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: Miguel Mazumder
    orcid: 0000-0003-1181-8118
    affiliation: 2
  - name: NAME
    orcid: 0000-0000-0000-0000
    affiliation: 2
  - name: NAME
    orcid: 0000-0000-0000-0000
    affiliation: 2
affiliations:
  - name: First Affiliation
    index: 1
  - name: Soka University
    index: 2

    
date: 19 September 2025
cito-bibliography: paper.bib
event: BH25JP
biohackathon_name: "DBCLS BioHackathon 2025"
biohackathon_url:   "https://2025.biohackathon.org/"
biohackathon_location: "Mie, Japan, 2025"
group: Glyco MCP Server
# URL to project git repo --- should contain the actual paper.md:
git_url: [https://github.com/biohackathon-japan/bh25-bhxiv-template](https://github.com/biohackathon-japan/BH25-Glyco-MCP-server)
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Mazumder M., Priscilla J. \emph{et al.}
---

# Introduction

As part of the DBCLS BioHackathon 2025, we are here to report on behalf on the Glyco MCP server project team. The aim of this project is to investigate how MCPs (Model Context Protocols) can be applied to facilitate the research query process between GlyCosmos and PubChem. By integrating glycan-related data (structures, synthesis genes, glycoprotiens, and glycolipids) through extensive SPARQList resources, we aim to enable natural language access to these datasets. This approach lowers the barrier for researchers unfamiliar with SPARQL or RDF, while supporting reproducible and modular workflows.

While GlyCosmos provides rich programmatic access to glycans, genes, glycoprotiens and related information through SPAQRL queries and SPARQList endpoints, practical use of this access requires detailed knowledge of their parameters, query syntax, and JSON outputs. Similarity, while PubCHem offers chemical identifies and structures through its own APIs, integrating these with glycoinformatics resources requries writing multi-step federated queries in SPARQL or custom scripts. For many researchers with biology or chemistry background, this can appear as a steep learning curve with high risk of fragile workflows. For example, GlyCosmos currently organizes data across more than 150 RDF graphs, each of which may need to be addressed differently depending on the query, or point to specific information that a researcher may not be aware exists in that graph.

As a result, users will often default to manual browsing of GlyCosmos or GlyTouCan web portals. While these interfaces are valauable for preliminary explorartoy serachers, they have little flexibility when researchers need to perform specific actions such as :
- chain multiple queries (e.g disease -> gene -> glycan -> PubChem ID)
- retreive structued outputs as scale
- apply the same query across multiple different IDs

To address this gap between glyco researchers and complex retrieval of information from Glycosmos, we intend of implementing a mapping of natural language questions to existing GlyCosmos SPARQList APIs. This will allow researchers to ask questions such as species to glycan association, WURCS and GlycoCT sequences for a Glytoucan ID, or Disease to glycan association and retrive associated PubChem compounds. Instead of manually browisng or construction of SPARQL queries, these questions are automatically resolved into API calls with the approriate parameters. This approach offers a more inuitive and simple form of access to Glycosmos and PubChem.

Our work demonstrates how MCP servers can serve as a middleware layer than translates researcher-freindly natural language queries into SPARQL queries via SPARQList endpoints, enabling for a more robust integration acrses GlyCosmos and PubChem resources.

# Methodology
Our team approached this project as relative newcomers to Model Context Protcols (MCPs), SPARQL queries, and RDF data integration. 

To lower the barrier

With no very limited experience iwth Glycosmos, exploring the existing GlyCosmos SPARQList APIs was necessary to understand the predefines SPARQL queries available for mapping. An obstacle during this process is that of the 373 SPARQList API endpoints, only 81 are avavilable. 

# Results

# Discussion

# Future Directions

Beyond programmatic integration, the project alsoexplored outreach to experimental reserachers. Glycan projdcts used in laborites while avialble from many companies, often have unclear information where a given glycan can be purcahsed. With integration 
...

## Acknowledgements

...

## References

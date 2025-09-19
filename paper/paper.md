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

As part of the DBCLS BioHackathon 2025, we are here to report on behalf on the Glyco MCP server project team. The aim of this project is to investigate how MCPs (Model Context Protocols) can be applied to facilitate the research query process between GlyCosmos and PubChem. By integrating glycan-related data (structures, synthesis genes, glycoproteins, and glycolipids) through extensive SPARQList resources, we aim to enable natural language access to these datasets. This approach lowers the barrier for researchers unfamiliar with SPARQL or RDF, while supporting reproducible and modular workflows.

While GlyCosmos provides rich programmatic access to glycans, genes, glycoprotiens and related information through SPAQRL queries and SPARQList endpoints, practical use of this access requires detailed knowledge of their parameters, query syntax, and JSON outputs. Similarity, while PubCHem offers chemical identifies and structures through its own APIs, integrating these with glycoinformatics resources requries writing multi-step federated queries in SPARQL or custom scripts. For many researchers with biology or chemistry background, this can appear as a steep learning curve with high risk of fragile workflows. For example, there are 150 GRAPHS

As a result, users will often default to manual browsing of GlyCosmos or GlyTouCan web portals. While these interfaces are valauable for preliminary explorartoy serachers, they have little flexicy when reseracheds need to perform specific actions such as :
- chain multiple queries (e.g disease -> gene -> glycan -> PubChem ID)
- retreive structued outputs as scale
- apply the same query across multiple different IDs

To address this gap between glyco reserachers and complex retrieval of information from Glycosmos, 
# Results


# Discussion

# Future Directions
...

## Acknowledgements

...

## References

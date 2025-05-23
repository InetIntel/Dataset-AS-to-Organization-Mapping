# Dataset: AS to Organization mapping (IIL-AS2Org)

This repo contains historical and current versions of our AS to Organization mapping datasets. 

The methodology we use is described in the paper *Improving the Inference of Sibling Autonomous Systems* published at the [Passive and Active Measurement Conference (PAM) 2023](https://pam2023.networks.imdea.org/program/). This dataset won the PAM 2023 Best Community Artifact Award. 

Please create issues to report any inaccuracy in the dataset!

The dataset is organized per ASN and each ASN is associated with the following columns: 
- **Status** (matched / unmatched (orphan) / no hint of error / Manual) 
- **Reference Orgs** (the list of dictionaries of our output related organizations) 

  - There are three main types of dictionaries: {"source": "Whois", "name": "xxx"}, {"source": "PDB", "name": "xxx", 'org_id': "xxx"}, and {"source": "CA2O", "url": "http://api.asrank.caida.org/v2/restful/organizations/xxx"}. For the third type, when CA2O makes a different inference other than the Whois organization, we provide the link to CAIDA ASRank restful API of the inferred organization. When CA2O does not have an inferred organization, we provide the link to CAIDA ASRank restful API of the ASN object, i.e., {"source": "CA2O", "url": "http://api.asrank.caida.org/v2/restful/asns/xxx"}.

- **Sibling ASNs** (our inferred sibling ASNs) 
- **PDB.org** (PDB-mapped organization, from PDB dataset)
- **PDB.org_id** (PDB-mapped organization's ID, from PDB dataset)
- **Name** (AS-name in Whois, from Whois dataset)
- **Descr** (Description field in Whois, from Whois dataset)
- **Website** (Website URL of the ASN, from PDB or BGP.tools)
- **Comparison with CA2O** (Agree / Disagree)
- **Comparison with PDB** (Agree / Disagree)

# LICENSE

See the [LICENSE](LICENSE) file for more info.


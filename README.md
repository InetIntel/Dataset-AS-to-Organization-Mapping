# Improving-Inference-of-Sibling-ASes

This repo contains the generated dataset from the paper *Improving the Inference of Sibling Autonomous Systems* accepted by Passive and Active Measurement Conference (PAM) 2023. This dataset won the PAM 2023 Best Community Artifact Award. Please create issues to report any inaccuracy in the dataset!

The dataset is organized per ASN and each ASN is associated with 8 columns: 
- **Status** (matched / unmatched (orphan) / no hint of error) 
- **Reference Orgs** (the list of our output related organizations) 
- **Sibling ASNs** (our inferred sibling ASNs) 
- **CA2O.Org** (CA2O-mapped organization, from CA2O dataset) 
- **PDB.Org** (PDB-mapped organization, from PDB dataset)
- **Name** (AS-name in Whois, from Whois dataset)
- **Descr** (Description field in Whois, from Whois dataset)
- **Website** (Website URL of the ASN, from PDB or BGP.tools).

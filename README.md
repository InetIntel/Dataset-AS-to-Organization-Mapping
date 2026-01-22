# Dataset: AS to Organization mapping (IIL-AS2Org)

This repo contains historical and current versions of our AS to Organization mapping datasets. 

The methodology we use is described in the paper *Improving the Inference of Sibling Autonomous Systems* published at the [Passive and Active Measurement Conference (PAM) 2023](https://pam2023.networks.imdea.org/program/). This dataset won the PAM 2023 Best Community Artifact Award. 

Please create issues to report any inaccuracy in the dataset!

**From 2025-06, we use an updated dataset format and generation methodology. (referred to as ii.as-org.v02)**

[![DOI](https://zenodo.org/badge/563047649.svg)](https://doi.org/10.5281/zenodo.18340700)

## New format and methodology
The dataset is organized per **ASN** and each ASN is associated with the following columns: 
- **Status** (matched / unmatched (orphan) / no hint of error / Manual) 
- **Reference Orgs** (the list of dictionaries of our output related organizations) 

  - There are ONLY two types of dictionaries: {"source": "Whois", "name": "xxx"}, {"source": "PDB", "name": "xxx", 'org_id': "xxx"}. Our updated methodology does not rely on CAIDA AS2Org anymore. We generate Whois AS2Org based on bulk whois data and conduct pool detection and the following steps based on it.

- **Sibling ASNs** (our inferred sibling ASNs)
- **Whois.org** (Whois-mapped organization, from bulk Whois files)
- **PDB.org** (PDB-mapped organization, from PDB dataset)
- **Name** (AS-name in Whois, from Whois dataset)
- **Descr** (Description field in Whois, from Whois dataset)
- **Website** (Website URL of the ASN, from PDB or BGP.tools)

## Old format and methodology
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

## Citation

If you use this dataset, please cite the Zenodo **concept DOI** (all versions):
https://doi.org/10.5281/zenodo.18340700

```bibtex
@software{chen_as2org_concept,
  author       = {Chen, Zhiyi and
                  Bischof, Zachary and
                  Testart, Cecilia and
                  Dainotti, Alberto},
  title        = {AS to Organization Mapping (IIL-AS2Org)},
  month        = jan,
  year         = 2026,
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.18340700},
  url          = {https://doi.org/10.5281/zenodo.18340700},
  note         = {Concept DOI (all versions). For a specific snapshot/release, please cite the corresponding Zenodo version DOI.},
}
```

If you find the methodology or framework described in our paper useful, please also cite:
```
@inproceedings{chen2023improving,
  title        = {Improving the Inference of Sibling Autonomous Systems},
  author       = {Chen, Zhiyi and Bischof, Zachary S and Testart, Cecilia and Dainotti, Alberto},
  booktitle    = {International Conference on Passive and Active Network Measurement},
  pages        = {345--372},
  year         = {2023},
  organization = {Springer}
}
```

# LICENSE

See the [LICENSE](LICENSE) file for more info.


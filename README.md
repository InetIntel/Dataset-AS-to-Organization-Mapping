# Dataset: AS to Organization mapping (IIL-AS2Org)

This repo contains historical and current versions of our AS to Organization mapping datasets. 

The methodology we use is described in the paper *Improving the Inference of Sibling Autonomous Systems* (PAM 2023).
- [Publisher page (Springer)](https://link.springer.com/chapter/10.1007/978-3-031-28486-1_15)
- [Author accepted manuscript (PDF)](https://zhiyichenGT.github.io/Improving%20the%20Inference%20of%20Sibling%20Autonomous%20Systems%20(Accepted%20Manuscript).pdf)

This dataset won the PAM 2023 Best Community Artifact Award.

Please open an issue to report any inaccuracies in the dataset (include ASN, month, and evidence)!

[![DOI](https://zenodo.org/badge/563047649.svg)](https://doi.org/10.5281/zenodo.18340700)

## Quick start

- Latest snapshot: see the `data/` directory for monthly JSON snapshots.
- Recommended format for new users: `v1.2 + ff003` (no CAIDA-dependent fields).
- File naming: `IIL-AS2Org.v{method}.ff{format}.YYYY-MM.json`

## Methodology versions

### Version 1.0 (v1.0)

We refer to the methodology described in our PAM 2023 paper as version 1.0.

### Version 1.1 (v1.1)

Version 1.1 is a minor update to v1: we replaced the CAIDA AS Classification (CA2O) signal used in v1 with organization information derived from bulk Whois data.
As shown in our PAM'23 paper, CAIDA AS Classification differs from Whois for only a small fraction of ASes (~3% in APNIC and <1% in other RIRs), so we consider v1.1 a minor revision of v1.

### Version 1.2 (v1.2)

Version 1.2 is an update based on v1.1 with the following changes:
	1.	Added approximately 4,200 ASNs owned by the China Education and Research Network (CERNET) and its project, the Future Internet Technology Infrastructure (FITI), as sibling ASNs. These ASNs exist only in as-block objects (i.e., they are delegated) and do not have corresponding aut-num objects in Whois. Although similar cases also exist in the APNIC region and its NIRs (e.g., JPNIC and CNNIC), we make this exception only for CERNET. The reasons are twofold: (1) almost all of these 4,200 CERNET ASNs are routed, whereas such ASNs in RIRs/NIRs are rarely routed; and (2) these CERNET ASNs are actually used by CERNET and its project, making them true sibling ASNs. In contrast, similar ASNs held by RIRs/NIRs are typically only temporarily under their control, are not used by them, and have not yet been officially assigned to other organizations. Therefore, those ASNs should not be treated as siblings.
	2.	Updated the manual correction list used for sibling identification. Siblings identified through this list are labeled as Manual in the status field.
	3.	Fixed a bug so that ASNs assigned by JPNIC are now correctly included in the dataset.

## File Formats

### File Format 1 (ff001)

We refer the file format described in our PAM 2023 paper as ff001, as follows: 

The dataset is organized per ASN and each ASN is associated with the following columns: 
- **Status** (matched / unmatched (orphan) / no hint of error / manual) 
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

We initially generated the datasets in ff001 (using method v1.0) for snapshots before 2025-04. To ensure format consistency across all snapshots, we convert these ff001 files to ff002. However, because bulk WHOIS data are only available starting from the following dates—arin (2023-03-28), jpnic (2023-03-28), ripe (2023-03-28), apnic (2023-04-01), afrinic (2023-04-01), and lacnic (2024-07-19)—we use the nearest available WHOIS snapshot to populate the Whois.org field for earlier datasets. For ASes that do not appear in the nearest WHOIS snapshot, we set this field to "Unknown".

### File Format 2 (ff002)

This file format does not contain any field related to CAIDA AS Classification. The dataset is organized per **ASN** and each ASN is associated with the following columns: 
- **Status** (matched / unmatched (orphan) / no hint of error / Manual) 
- **Reference Orgs** (the list of dictionaries of our output related organizations) 

  - There are ONLY two types of dictionaries: {"source": "Whois", "name": "xxx"}, {"source": "PDB", "name": "xxx", 'org_id': "xxx"}. 

- **Sibling ASNs** (our inferred sibling ASNs)
- **Whois.org** (Whois-mapped organization, from bulk Whois files)
- **PDB.org** (PDB-mapped organization, from PDB dataset)
- **Name** (AS-name in Whois, from Whois dataset)
- **Descr** (Description field in Whois, from Whois dataset)
- **Website** (Website URL of the ASN, from PDB or BGP.tools)

### File Format 3 (ff003)

Methodology version 1.2 includes thousands of CERNET ASNs as sibling ASNs, making it inefficient to store the full Sibling ASNs field for every AS entry as in ff001 and ff002. To avoid this redundancy, we designed ff003 to separate organization-level information from ASN-level mappings.
```json
{
  "metadata": {
    "version": "v1.2",
    "file_format": "ff003",
    "snapshot_month": "2026-01",
    "documentation_url": "https://github.com/InetIntel/Dataset-AS-to-Organization-Mapping",
  },
  "organizations": [
    {"orgID": "xxx", "Reference Names": ["xxx"]},
    ...
  ],
  "as2org": {
    "AS1": {
      "OrgID": "xxx",
      "Status": "xxx",
      "Note": "xxx",
      "Whois.Org": "xxx",
      "PDB:Org": "xxx",
      "Name": "xxx",
      "Descr": "xxx",
      "Website": "xxx"
    }
  }
}
```
•	organizations: We create artificial orgIDs for each organization. These IDs have no real-world meaning and are used only within the dataset. Reference Names contains all relevant names associated with the organization that we found in Whois and PeeringDB.
•	as2org: We keep the same fields included in ff002.

## Dataset naming

We name our dataset based on the methodology version and file format version. For example, IIL-AS2Org.v1.0.ff001.2022-10.json means the dataset is generated using methodology version 1.0 in format 1. YYYY-MM indicates a monthly snapshot for that month.

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
  note         = {Concept DOI (all versions). For a specific snapshot/release, please cite the corresponding Zenodo *version DOI*.},
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

## LICENSE / Acceptable Use Agreement (AUA)

The dataset is publicly accessible in this GitHub repository. However, any access and use of the data is subject to the Acceptable Use Agreement (AUA) and license terms provided by Georgia Tech.

See the [LICENSE](LICENSE) file for details.

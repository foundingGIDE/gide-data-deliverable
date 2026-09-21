# GIDE Metadata Snapshot (D10.1)

Harmonized study-level metadata from three major bioimaging repositories — **BioImage Archive (BIA)**, **Image Data Resource (IDR)**, and **SSBD** — in one FAIR, queryable dataset.

* 📦 **Data:** https://zenodo.org/records/20922775
* 📄 **Report (D10.1):** https://zenodo.org/records/20807591

See also https://www.gide-project.org/portal for the data usage in GIDE. 

## What's inside

- **\> 1000 studies**, each as a JSON-LD [RO-Crate](https://www.researchobject.org/ro-crate/) (detached, v1.2)
- A combined RDF graph (Turtle) of all studies
- A SHACL shape for validating against the GIDE RO-Crate profile
- Species and imaging methods annotated with NCBI Taxonomy and FBbi ontology terms
- Example SPARQL queries and a ready-to-run local endpoint

## Files

| File | Description |
|---|---|
| `gide_profile.md` | Human-readable profile specification |
| `gide_profile_shacl_shape.ttl` | Machine-readable profile (SHACL) |
| `gide_metadata_combined.ttl` | All RO-Crates merged into one RDF graph |
| `gide_metadata_with_ontologies.ttl` | Combined graph + FBbi/NCBITaxon parent terms for hierarchical search |
| `gide_profile_validation.html` | SHACL validation report |
| `gide_ncbi_and_fbbi_validation.html` | Ontology term/label consistency report |
| `gide_sparnatural_template.ttl` | Config for the Sparnatural visual query UI |
| `Qleverfile` | Local SPARQL endpoint setup (QLever) |
| `Qleverfile-ui.yml` | QLever UI config with example queries |

## Data model (minimum)

Each study is a `schema:Dataset` that **must** link to:

- `schema:about` → the species studied (NCBI Taxonomy term recommended)
- `measurementMethod` → the imaging method (FBbi term recommended)

The full profile (aligned with REMBI) supports richer biosample, method, and descriptive metadata. See [D7.1](https://doi.org/10.5281/zenodo.20808012) for details.

> Metadata is study-level only; direct file download links are not included.

## Quick start (RDF graph)

1. Download the files from Zenodo.
2. Install [QLever](https://github.com/ad-freiburg/qlever).
3. Run `qlever index`, then `qlever start` using the provided `Qleverfile`.
4. Launch the UI with `Qleverfile-ui.yml` and try the example queries.

### Example query

Find studies by species and imaging method:

```sparql
SELECT DISTINCT ?studyName ?identifier ?species ?imagingMethod
WHERE {
  ?study a schema:Dataset ;
         schema:name ?studyName ;
         schema:identifier ?identifier ;
         schema:about ?species ;
         dwc:measurementMethod ?imagingMethod .
}
```

## Source pipelines

- BIA: https://github.com/BioImage-Archive/gide-ro-crate
- IDR: https://github.com/German-BioImaging/idr_study_crates
- SSBD: https://github.com/openssbd/gide-ro-crate

This repository harvests, validates, and combines their outputs.

## References

- D10.1: Harmonized metadata snapshot (this deliverable) — https://zenodo.org/records/20807591
- D6.1: Metadata model overlap and gaps — https://doi.org/10.5281/zenodo.16794787
- D7.1: Minimal shared interoperability metadata set — https://doi.org/10.5281/zenodo.20808012

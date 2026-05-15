# synapse-corpus-heavy

Large-scale PDF stress-testing corpora extracted, normalized, and repackaged from the PDF Association SafeDocs Stressful PDF Corpus.

This repository is intended for:

* heavyweight parser validation
* rendering engine regression testing
* large-scale fuzzing pipelines
* memory pressure analysis
* malformed PDF stress execution
* scheduled CI workloads

---

# Overview

Unlike lightweight corpora used during standard pull requests, the datasets in this repository are intentionally isolated due to their large size and high extraction cost.

These corpora are designed for:

* dedicated GitHub Actions runners
* nightly validation workflows
* scheduled regression testing
* deep parser compatibility verification

---

# Included Corpora

Current datasets include:

* PDFBOX
* GHOSTSCRIPT
* MOZILLA
* LIBREOFFICE

Each dataset is packaged independently as a normalized `.zip` archive to allow selective downloads during CI execution.

---

# Why This Repository Exists

The original SafeDocs corpus distribution is extremely large and inefficient for modern CI pipelines.

This repository exists to:

* avoid downloading monolithic multi-gigabyte archives
* reduce GitHub Actions storage pressure
* isolate heavyweight test suites from lightweight PR validation
* improve reproducibility for parser and renderer testing
* enable deterministic corpus fetching inside automated workflows

---

# Repository Structure

```txt id="i3yeql"
synapse-corpus-heavy/
├── README.md
├── LICENSE
├── manifest.json
├── SHA256SUMS
├── pdfbox.zip
├── ghostscript.zip
├── mozilla.zip
└── libreoffice.zip
```

---

# Usage Example

Download only the required corpus during CI execution:

```bash id="blt9kr"
mkdir -p tests/assets/corpus/pdfbox

curl -L \
  https://media.githubusercontent.com/media/YOURORG/synapse-corpus-heavy/main/pdfbox.zip \
  -o pdfbox.zip

unzip -q pdfbox.zip -d tests/assets/corpus/pdfbox/

rm pdfbox.zip
```

---

# GitHub Actions Example

```yaml id="6n17zd"
- name: Fetch PDFBOX Corpus
  run: |
    mkdir -p tests/assets/corpus/pdfbox

    curl -L \
      https://media.githubusercontent.com/media/YOURORG/synapse-corpus-heavy/main/pdfbox.zip \
      -o pdfbox.zip

    unzip -q pdfbox.zip -d tests/assets/corpus/pdfbox/

    rm pdfbox.zip
```

---

# Recommended CI Strategy

Because these corpora are significantly larger than standard datasets, the recommended workflow strategy is:

* sequential execution
* dedicated runners
* scheduled workflows
* nightly or manual dispatch execution

Example triggers:

```yaml id="uqc02g"
on:
  workflow_dispatch:

  schedule:
    - cron: "0 4 * * *"
```

---

# Optimization Notes

Each corpus was repackaged to:

* remove unnecessary metadata
* eliminate nested archive duplication
* reduce decompression overhead
* improve CI extraction speed
* minimize temporary disk usage

Only normalized archives are stored.

Raw upstream distributions and extracted intermediate artifacts are intentionally excluded.

---

# Provenance

The original datasets originate from:

* PDF Association SafeDocs Stressful Corpus
* https://labs.pdfa.org/stressful-corpus/

This repository redistributes normalized subsets strictly for testing, interoperability research, parser validation, and CI reproducibility purposes.

All rights remain with their respective upstream authors and projects.

---

# Integrity Verification

SHA256 hashes are provided inside:

```txt id="74r6js"
SHA256SUMS
```

Example verification:

```bash id="b1v5ra"
sha256sum -c SHA256SUMS
```

---

# Intended Usage

Recommended use cases include:

* PDF parser development
* renderer compatibility validation
* malformed PDF analysis
* fuzzing infrastructure
* regression testing
* differential parser testing
* memory pressure benchmarking
* security research

---

# License

Repository tooling, manifests, and packaging:
MIT

Corpus contents:
Owned by their respective upstream projects and contributors.

```
```

# Installation

```bash
pip install -r requirements
pip install git+https://github.com/acl-org/aclpubcheck
brew install mactex
# Install java
```

# Steps to generate Proceedings

```bash
# Copy existing example into AISD one [ALREADY DONE]
rm -rf examples/aisd
cp -r examples/sigdial examples/aisd

# Prepare program committee [ALREADY DONE]
python or2program_committee.py {YOUR-OR-EMAIL} {YOUR-OR-PASS} aclweb.org/NAACL/2025/Workshop/AISD

# Copy program_committee metadata/yml [ALREADY DONE]
cp program_committee.yml examples/aisd/papers/program_committee.yml
# ^^ manually remove removed reviewers and Harsh as a reviewer (was for testing).

# Download paper PDFs and metadata/yml
python openreview/or2papers.py {YOUR-OR-EMAIL} {YOUR-OR-PASS} aclweb.org/NAACL/2025/Workshop/AISD --track "Archival regular" --pdfs

# Copy papers PDFs
rm -rf examples/aisd/papers
cp -r papers examples/aisd/papers

# Copy papers metadata/yml
cp papers.yml examples/aisd/papers.yml

# Check paper PDFs
## First, manually make sure none of them are review versions, and then manually for each paper run:
aclpubcheck --paper_type other examples/aisd/papers/{NUMBER}.pdf

# Update all fields in all text and yaml files examples/aisd/papers/ in manually.

# Generate proceedings
./bin/generate examples/aisd --proceedings --overwrite # The output will be in outputs/. Check outputs/proceedings.pdf

# Compress, upload, and share with conf.
zip -r AISD_data.tgz output/
```

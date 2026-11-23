# DSA Reports Library: archive of copies

This repository holds Tech Policy Press's copies of the documents in the [DSA Reports Library](https://dsa-reports-library.onrender.com). The documents are risk assessments, risk mitigation reports, audit reports and audit implementation reports that very large online platforms and search engines publish under the EU Digital Services Act.

Links to these documents often stop working within months. The library keeps its own copy of every version it has seen, so every citation it gives keeps working. The weekly build never deletes anything; a document is removed only by hand, in response to a takedown request (see below).

Sources: Open Terms Archive and contributors (ODC-By 1.0), curated with CheckFirst; document index by Alexander Hohlfeld; platform publications. Compiled by Tech Policy Press with Mark Scott.

This library is a research aid. Its text is machine-extracted from documents published by the platforms and archived by Open Terms Archive and Tech Policy Press, and it may contain errors or omissions. Always check the original document before quoting or relying on anything here.

## Where the files are

All files are **release assets**. Git history holds only this README.

| Release | What it holds |
|---|---|
| `archive-0` through `archive-f` | The documents, one asset per file, named `{sha256}.{ext}` (`pdf`, `html` or `zip`). A file goes on the release whose tag ends in the first hex digit of its SHA-256. GitHub allows at most 1,000 assets per release, so the files are split 16 ways. |
| `state` | `manifest.json` (the library's full record of every document and source), `manifest.csv` (the same, for people) and `stats.json` (the last build's counts). |
| `cache-0` through `cache-f` | The text-extraction cache, `extracted__{sha256}.jsonl.gz`, split the same way. It's for the weekly build, not for readers. |

Files are named by their SHA-256 hash, so a file never changes once it is uploaded. A new version of a document is a new file. The old one stays, marked as superseded in the manifest.

## Finding a document

1. Download `manifest.csv` from the [`state` release](https://github.com/Team-Tech-Policy-Press/dsa-reports-library-archive/releases/tag/state).
2. Find the row by platform, document type and cycle year. The `doc_id` column is the library's permanent document ID. `original_urls` lists where the platform published the document, and `sources` lists where the library found it and when.
3. The `archive_asset` column gives the release and file name, for example `archive-a/a3f…e1.pdf`. Download it from `https://github.com/Team-Tech-Policy-Press/dsa-reports-library-archive/releases/download/{archive_asset}`.

Most people should use the library's site instead. There, `https://dsa-reports-library.onrender.com/archive/{doc_id}.pdf#page=N` opens a document at a cited page.

The searchable database and the bulk dataset (`library.sqlite`, `documents.csv`, `platforms.csv` and `passages.jsonl`) are published each week as releases of [Team-Tech-Policy-Press/dsa-reports-library-data](https://github.com/Team-Tech-Policy-Press/dsa-reports-library-data/releases), and `data-latest` always points to the newest.

## Takedown requests

If you hold rights in a document here and want it removed, contact contributions@techpolicy.press.

How a takedown is carried out. The build never deletes anything, so removal is a manual step by a maintainer:

1. Add the document to `dsalib/config/suppressed.yml` in the (private) code repository (its `sha256` or `doc_id`, the reason and the date), and commit. From then on the weekly build never archives or uploads that file again, leaves it out of the database, the dataset and `manifest.csv`, and the library's `/archive/{doc_id}` link answers 410 Gone. Its record stays in `manifest.json`.
2. Run the weekly workflow (or wait for it), so the site and the data releases drop the document.
3. By hand, in this repository's releases, delete the file's asset `{sha256}.{ext}` from `archive-{first hex digit}` and its extraction cache `extracted__{sha256}.jsonl.gz` from `cache-{first hex digit}`. Suppressing a ZIP covers the parts listed under it; delete each part's asset too.
4. Older dated releases in the data repository (`data-YYYY-MM-DD`) still hold the document's text. Delete those releases' assets by hand if the request covers the text as well.

# Bibliography

This directory contains the file `references.bib`, which stores **metadata for all raw sources** (`raw_sources/`) used in the thesis.  

## Purpose

- Keep bibliographic data separate from PDFs and notes
- Ensure **consistent citation keys**
- Allow notes and the thesis to reference sources in a uniform, reproducible way
- Make it easy to generate references in LaTeX, Markdown, or Pandoc

---

## Reference Types

- `@article` – Published academic article in a journal  
  *Example:* peer-reviewed papers from journals, conference proceedings published as journal papers

- `@inproceedings` – Conference paper  
  *Example:* papers presented at conferences not published in journals

- `@book` – Complete book or monograph  
  *Example:* textbooks, reference books, or academic monographs

- `@inbook` – Chapter or section of a book  
  *Example:* a single chapter of a multi-author edited volume

- `@misc` – Unpublished article, working paper, or arXiv preprint  
  *Example:* preprints, white papers, unpublished reports

- `@online` – Web page or online resource  
  *Example:* websites, blogs, or online reports

- `@techreport` – Technical report from a lab or institution  
  *Example:* internal reports, research institute publications

**Guidelines:**
- Use the type that best reflects the **source’s nature**.  
- Avoid using `@misc` unless the source is truly informal or unpublished.  
- Keep entries **consistent** with your PDF naming and citation key convention.

---

## Citation Keys

- Format: `firstauthorYYYYshorttitle`  
- Rules:
  - Lowercase only
  - First author only
  - Year mandatory
  - Short, meaningful title fragment
- Keys must remain stable throughout the project

---

## Example Entry

```bibtex
@article{grossman1980efficientmarkets,
  title   = {},
  author  = {},
  journal = {},
  year    = {},
  volume  = {},
  number  = {},
  pages   = {}
}

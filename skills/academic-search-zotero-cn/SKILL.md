---
name: academic-search-zotero-cn
description: End-to-end Chinese academic literature workflow that searches CNKI and web/English scholarly sources, collects paper titles and abstracts, imports selected records into Zotero, enriches Zotero items with abstracts and Chinese translation notes, and drafts an introduction-style synthesis in Chinese. Use when the user asks to find Chinese/English papers, import papers into Zotero, add abstracts or translated notes, or summarize papers as “XXX did what, obtained what results”.
---

# Academic Search Zotero CN

## Overview

Use this skill for a complete literature-to-Zotero workflow for Chinese-speaking academic users:

1. Search CNKI for Chinese literature and web/scholarly sources for English literature.
2. Select papers by relevance, recency, citation count, source quality, or the user's criteria.
3. Import selected records into Zotero.
4. Add abstracts to Zotero items.
5. Add a child note with title/abstract translation when the paper is English.
6. Draft an introduction-style synthesis: “Author/year did what, used what method/data, obtained what result, and why it matters.”

## Required Companion Skills

When the workflow needs CNKI, use `$cnki-codex` and its routed sub-skills.

When the workflow needs Zotero import, export, inventory, children, attachment, or citation work, use `$Zotero` / `$zotero` plugin capabilities.

When the workflow needs English or web scholarly search, use available scholarly search skills/tools first. If no academic MCP tools are available, use public web sources and scholarly APIs where allowed, such as Semantic Scholar, CrossRef, OpenAlex, publisher DOI pages, and ordinary web search.

## Workflow

### 1. Clarify Search Scope

Extract these fields from the user request:

- Topic and synonyms in Chinese and English.
- Time range.
- Target language: Chinese, English, or both.
- Selection rule: high citation, core journals, review papers, methods papers, recent work, or a fixed count.
- Zotero destination: current library/collection unless the user says otherwise.

If the user already gave enough information, do not ask. Make a conservative search strategy and proceed.

### 2. Search CNKI And Web Sources

For Chinese literature:

- Use `$cnki-codex` as the entry point.
- Use `cnki-search-codex` for normal paper search.
- Use `cnki-advanced-search-codex` when the user asks for CSSCI, 北大核心, CSCD, date filters, authors, journals, or source categories.
- Use `cnki-collect-details-codex` when abstracts, keywords, fund information, or rich metadata are needed.
- Stop and ask the user to solve CNKI captcha if it appears.

For English literature:

- Prefer Semantic Scholar for citation-count-sensitive discovery.
- Use CrossRef/OpenAlex/DOI pages to verify DOI, venue, year, authors, and abstracts.
- Use publisher pages or trustworthy indexed pages only to fill missing abstracts.
- Do not invent missing abstracts. Mark unavailable metadata clearly.

### 3. Select Papers

Deduplicate by DOI first, then normalized title.

Rank by the user's criteria. If the user asks for “highly cited”, rank by citation count but manually remove off-topic false positives.

For each candidate keep:

- Title
- Authors
- Year
- Journal/source
- DOI or URL
- Citation count and source, if used
- Abstract and abstract source
- Selection reason

### 4. Import Into Zotero

Start with Zotero readiness:

```bash
python <zotero-plugin>/skills/zotero/scripts/zotero.py status --json
```

If Zotero is not running or the local API is disabled, follow the Zotero skill instructions to enable and start it.

Import with the Zotero plugin when possible:

```bash
python <zotero-plugin>/skills/zotero/scripts/zotero.py import-bibtex --file selected.bib --yes
```

After import, verify with:

```bash
python <zotero-plugin>/skills/zotero/scripts/zotero.py inventory --json
python <zotero-plugin>/skills/zotero/scripts/zotero.py export-bibtex --out verification.bib
```

If Connector import times out, check the inventory before retrying. Zotero may have imported successfully despite a timeout.

### 5. Enrich Zotero Items

For each imported item:

- Add English abstract to Zotero `abstractNote` when available.
- If the paper is English, add one child note titled `中文题名与摘要翻译（Codex）`.
- The note should contain English title, Chinese title, English abstract, Chinese abstract, abstract source, and processing note.
- If the paper is Chinese, add a note only if the user asks for English translation or a reading note.

If the Zotero plugin helper cannot update existing fields or child notes directly, prefer supported Zotero/Connector write paths. If a local database update is necessary, do all of the following:

- Close Zotero first.
- Make a timestamped backup of `zotero.sqlite`.
- Update only the target items.
- Reopen Zotero.
- Verify with the Zotero plugin local API.

### 6. Draft Introduction-Style Synthesis

Read `references/note-and-intro-templates.md` when generating notes or the final synthesis.

Produce an introduction paragraph or bullet synthesis in Chinese. Use this structure:

- Research background/problem.
- Existing studies grouped by mechanism, assessment/modeling, monitoring/data, and mitigation if applicable.
- For each cited work: “Author/year did what, using what method/data, found what result.”
- Gap and transition to the user's study.

Do not overstate causality or novelty. Keep citation claims aligned with the collected abstracts.

## Validation Checklist

Before final response, verify:

- Search sources used and limitations are clear.
- Imported Zotero item count matches the selected paper count.
- Each target Zotero item has DOI or URL.
- Each target Zotero item has an abstract or a clear “not publicly found” note.
- English papers have Chinese title/abstract translation notes.
- A backup path is reported if Zotero was modified outside the plugin helper.
- Final answer lists what was imported/enriched and where exported files are saved.

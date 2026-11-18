# Secret scan

Scanned 2026-11-18 (America/Chicago), before publication. Scope: every file in this
repository (PDF, Markdown rendering, README.md, LICENSE, NOTICE).

## Method

- PDF structure: `pdfdetach -list` (embedded files), `pdfimages -list` (images),
  check for /EmbeddedFile, /JavaScript, /URI, /Launch, /OpenAction markers, and a
  read of the document Info dictionary.
- All 26 PDF content streams were decompressed and searched, as well as the raw PDF
  bytes and the extracted text (`pdftotext -layout`).
- Pattern search on all text: salt, password / passwd / pwd, username / login,
  api key, secret, token, bearer, private key blocks, AWS key IDs, GitHub tokens,
  `sk-` keys, long hex strings (32+), long base64 runs (40+), email addresses,
  phone numbers, URLs, IP addresses.
- There are no zip, gz or other archive files in this repository.

## Results

| Check | Result |
|---|---|
| Embedded files / attachments in PDF | None |
| Images in PDF | None |
| JavaScript, launch actions, URI links in PDF | None |
| PDF Info dictionary | Producer `iOS Version 27.2.1 (Build 24B156) Quartz PDFContext`, CreationDate and ModDate 2026-11-17 02:11:20 UTC (Mon Nov 16 20:11:20 2026 CST). No author, title or user fields |
| Salts, passwords, usernames, keys, tokens | None found |
| Email addresses, phone numbers, IP addresses | None found |
| Long hex values | The PDF's own SHA-256 (cited in README and the rendering) and the PDF trailer /ID `3ff105e3b6914f4c57b78a2a58771acc`, a standard document identifier. Not secrets |
| Frozen-package hashes in the record | SHA-256 prefixes only (`ca08de0f…`, `5c32a9e3…`, `0ebb4237…`), as printed in the record. Not secrets |
| False positives reviewed | `pwd` inside compressed font bytes; "phone-like" number runs that are font bounding boxes and page-drawing coordinates in the decompressed content streams (for example `125 108.5332`); `/AA` matches that are font subset names (`/AAAAAB+…`), not additional-action entries; the word "SECRET" in README (this file's name) |
| Personal information | Author name and city/state (Tulsa, OK) as printed in the record. Named people credited by the record: Jean-Guillaume Nardi, Donald Paul Smith |

Re-run 2026-11-18 over every file after the copyright wording changed to Soulshine alone: same results. This file's own method list matches its search terms, as expected.

Nothing was withheld.

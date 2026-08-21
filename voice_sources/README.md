# Voice sources

Place any user-selected papers or writing samples for voice matching in this directory. Compatible reference files may be in practical formats such as PDF, DOCX, TXT, or Markdown.

When a request explicitly names a file, use that file. Otherwise, when voice matching is requested, use the suitable files in this directory.

For cross-sample validation, place two or more independent samples here and leave them as separate files.
The skill analyzes each selected file separately before comparing recurring and context-dependent patterns.
Patterns supported by only one source remain provisional and do not become general voice rules.

Infer only style features such as sentence rhythm, paragraph structure, transitions, punctuation, formality, and hedging. Never copy distinctive wording or import facts, claims, results, citations, references, or structure-specific content from a voice source.

## Examples

- `Match my voice using voice_sources/prior_paper.pdf.`
- `Use voice_sources/writing_sample.docx as the voice reference.`
- `Match my voice using the suitable files in voice_sources/.`

Keep this directory generic. Do not create separate folders for individual people, author voice, disciplinary register, or generated profiles.

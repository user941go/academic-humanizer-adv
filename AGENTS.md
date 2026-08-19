# Voice sources

- Treat every compatible file under `voice_sources/` as a user-selected voice reference.
- When a task explicitly names one or more files, use those files. Otherwise, when voice matching is requested, use the suitable files in `voice_sources/`.
- Infer only style features, such as sentence rhythm, paragraph structure, transitions, punctuation, formality, and hedging.
- Never copy distinctive wording or import facts, claims, results, citations, references, or structure-specific content from a voice source.
- Practical supported formats include PDF, DOCX, TXT, and Markdown.
- Keep `voice_sources/` generic: do not create separate folders for individual people, author voice, disciplinary register, or generated profiles.

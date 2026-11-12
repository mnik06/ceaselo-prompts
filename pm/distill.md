Split each client document below into sections so a project manager can find the part they need without reading it all.
Every line is prefixed with its line number and "| ". Choose where each section starts.

{{documents}}
Rules, all checked by machine:
- Sections follow the document's own structure: a heading, a topic change, a new speaker turn or agenda item in a transcript.
- At most 200 sections per document; a short document may be a single section.
- startLine is a line number of that document, ascending; the first section starts at line 1.
- title: at most 80 characters. summary: ONE sentence, at most 200 characters, saying what the section contains, not what it is called.

Answer with one JSON object and nothing else: {"documents":[{"index":<document index>,"sections":[{"startLine":1,"title":"...","summary":"..."}]}]}

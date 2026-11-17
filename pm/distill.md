Split each client document below into sections so a project manager can find the part they need without reading it all.
Every line is prefixed with its line number and "| ". Choose where each section starts.

{{documents}}
Rules, all checked by machine:
- Sections follow the document's own structure: a heading, a topic change, a new speaker turn or agenda item in a transcript.
- At most 200 sections per document; a short document may be a single section.
- startLine is a line number of that document, ascending; the first section starts at line 1.
- title: at most 80 characters. summary: ONE sentence, at most 200 characters, saying what the section contains, not what it is called.

Answer with one JSON object and nothing else: {"documents":[{"index":<document index>,"sections":[{"startLine":1,"title":"...","summary":"..."}]}]}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the material (40, "material read"), and last, the moment you start writing your final answer (60, "writing the answer"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.

{{designKit}}

{{designMethod}}

{{designRules}}

{{designSystem}}

# Revise the prototype of "{{projectName}}"

Code assembles one offline HTML file from the design system, the app shell, the sample data and every screen of the plan. A member of the project asked for changes; you edit only the part named below, in your workspace. Everything else is copied unchanged into the next version.

Design brief:
{{brief}}

App shell (`shell.html`):
{{shell}}

Sample data (`data.js`):
{{data}}

Screen plan (every route that exists):
{{plan}}

# Your part: {{part}}
{{target}}

{{designTarget}}

What was asked for:
{{notes}}

Requirements these screens show (read any other with kb_get):
{{requirements}}

## Rules

- Change what was asked for and what it takes to do it well; keep everything else as it is: copy, data, links, states and roles.
- When the notes ask for a different layout of a screen, rewrite that screen from its plan entry, the brief and the notes instead of patching it; keep its copy, data, links, states and roles.
- Take every action label, toast, entity name and empty or error line from `APP_DATA.copy`; a word you need that it lacks follows its pattern.
- A change that needs a new field, rule, role or flow the requirements do not have is a requirement change: do not build it. Put one line per such change in `flags.json` (what was asked and why it changes the requirements); Kip takes it up with the people. Wording, layout, emphasis, order, empty and error copy and visual changes are yours to make.
- A screen is its content only: one element data-state="<state>" per state its plan entry lists. Link to every route its entry lists in "links", with href="#/<route>"; link only to planned routes.
- The shell keeps exactly one element data-slot="screens" and its data-slot="logo"; navigation reaches every top-level screen.
- Preview every state of every screen you changed at its viewports, and every route's default state when you changed the shell, with `prototype_preview` (6 views per call), and judge each view as its user would: does it lead with the screen's one job; is there one primary action; does any state read as empty or broken; is there a generated-page tell (identical cards for everything, an all-caps label above every heading, middle-dot meta, an accented headline word, "→" on links); does anything clip, crowd or misalign at the phone width. Then remove one decoration that does not serve the screen. Fix, and re-preview what you changed; code refuses the answer if a view is missing. Then call `prototype_check` if it is listed and fix every reason it returns before you answer.
- Answer with one short sentence once the files are edited.{{rejected}}

## Progress

People watch this task's card and Kip's pill. Call `progress_report` with `percent` and a short `note` (at most 80 characters, plain words) at these milestones only, then carry on without waiting: right after reading the ask and the requirements (25, "ask read"), once every change is made (55, "changes made"), and last, when you start previewing (70, "previewing the changes"). Report each milestone the moment you reach it, never several at once later; never call it once your answer has begun, never more often, never with 100 (the end of the task says that), and skip it if the tool is not listed.

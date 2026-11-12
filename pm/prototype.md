Build a clickable, low-fidelity prototype of "{{projectName}}" as ONE self-contained HTML file.

Baseline summary (read doc_section and the kb_* tools for detail):
{{baselineSections}}

Key decisions:
{{decisions}}{{requestedChange}}

Rules, all checked by machine:
- One file, at most 2 MB. Inline all CSS, JS and data. No external URL anywhere: no src or href to http(s) or relative files, no @import, no url() other than data: URIs.
- Every screen is an element with data-screen="<route>", data-title="<screen name>" and data-summary="<one line>". Navigation uses hash routes (href="#/<route>"); show the screen whose route matches location.hash.
- A mobile screen also carries data-device="mobile" and is drawn inside a phone frame (rounded bezel, notch, about 390px wide) centred on the page.
- Low fidelity: real labels and realistic sample data, no brand polish.

Answer with the HTML document only.{{rejected}}

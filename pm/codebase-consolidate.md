You are the Project Manager agent of "{{projectName}}", an existing software project made of several repositories, each analysed on its own:
{{repos}}

Each analysis named features, roles and entities in its own words, so one capability can appear twice under two slugs (the api's "user-auth" and the web app's "sign-in"), one role under two names, and one entity once per repo. Unify them so the Project Spec reads as one product.

## Everything read from the code (key [type] (tags) repo: title — summary)
{{index}}

Use kb_get on any key whose body you need to decide. Then answer:
- features: one rename per slug that names the same capability as another, from the slug to drop to the slug to keep (the clearer, user-facing one). Never merge two capabilities that only look alike.
- roles: the same for role slugs in the Roles decision.
- drop: items that say the same thing as another item (the same entity read in two repos, the same requirement stated from the server and from the screen, the same decision), each with the key it duplicates; keep the fuller one. Never drop an item that adds something the other lacks.

Answer with one JSON object only:
{"features": [{"from": "", "to": ""}], "roles": [{"from": "", "to": ""}], "drop": [{"key": "", "duplicateOf": "", "why": ""}]}

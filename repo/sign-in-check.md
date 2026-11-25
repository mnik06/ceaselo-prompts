You are checking that agents can sign in to the running app of the repository {{repo}}, so its captures, builds and verifies never stall at its sign-in. Your working directory is the repository's checkout; the app is already running on its own throwaway database, and the browser tools drive one browser the machine started for you. You never edit, commit or push a file, never change the app's code or data through code, SQL or an API call, never create a record, and never start another server.

The accounts to check are in your environment: `$CEASELO_LOGINS` is a JSON list of `{"role", "email", "password"}`, one per account. Read it with Bash, type each value into the app's own fields, and never print or repeat a password.{{roles}}

## What you do

1. For each account: open the app, sign in through its own sign-in page, and see whether you are signed in. When the app refuses the account, keep its own error message as the page shows it. Sign out before the next account.
2. With the first account that signed in, open the app's navigation (header, sidebar, menus) and open every page a signed-in person reaches from it, at most 30, main ones first. A page that shows its content is reached; one that shows an error, a "not allowed" message, or sends you back to sign-in is not, with why in a few words.
3. Never complete a step for the account (an onboarding form, a profile, creating an organisation): agents must land in the app as it is. When every main page sends a signed-in account to such a step, or it reaches no page of the app's own content, set `blocked` to what the account lacks (for example "every page redirects to /welcome, which asks for a display name").

## Answer

End with one JSON object only:
{"accounts": [{"role": string, "ok": boolean, "error": string | null}], "reached": [string], "unreached": [{"route": string, "why": string}], "blocked": string | null, "failure": string | null}
`reached` lists routes as the app names them (`/projects/:id` for a page with an id). `failure` says in one plain sentence a person can act on why no account could be checked (`$CEASELO_LOGINS` is empty, the app never showed a sign-in, the app did not load), else null.

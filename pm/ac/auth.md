### Block `auth`: sign-up, sign-in, recovery, session

- Wrong credentials are refused with one message that does not reveal whether the account exists.
- Repeated failed sign-ins are slowed or blocked after a stated number of attempts.
- A password shorter or weaker than the stated rule is refused on the field with the rule named.
- A signed-out person opening a protected screen is sent to sign-in and, once signed in, returns to that screen.
- Signing out ends the session; going back afterwards does not show protected content.
- An expired session sends the user to sign-in without losing the screen they were on.
- A recovery or verification link works once, expires after the stated time, and an expired or used link says so and offers a new one.

### Block `ui-mobile`: a GUI on phones (iOS, Android, or a PWA)

Every screen the ticket adds or changes on a phone target, in addition to `ui`.

- Every tappable control is at least 44 pt by 44 pt, and two controls never sit so close that one tap hits the wrong one.
- Content and controls stay inside the safe areas: nothing sits under the status bar, the notch, the camera cut-out or the home indicator.
- The OS back action (Android's back button, the back gesture, iOS's swipe from the edge) returns to the previous screen with its state, and never discards entered input without asking.
- Closing the app and opening it again returns the person to where they were, still signed in, with unsaved input kept or a statement that it was discarded.
- At the largest system text size, every text stays readable and nothing is cut off or overlaps.
- Where the requirements say the product works offline: without a connection the screen says so, keeps what is already loaded, and an action taken offline is either queued and sent when the connection returns or refused with a message saying it needs a connection.

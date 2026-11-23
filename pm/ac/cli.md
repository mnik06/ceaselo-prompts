### Block `cli`: command-line surface

Every command or option the ticket adds or changes.

- Asking for help (the help option, or the command with no arguments where the ticket says so) prints usage naming every command and option with one line each, and exits with status 0.
- An unknown command or option, or a missing or invalid argument, is refused with a message naming it and the usage line, and a non-zero exit status.
- A success exits with status 0, and every failure the ticket names exits non-zero, with the status the ticket states where it states one.
- Results go to standard output and nothing else; errors, warnings and progress go to standard error, so piping the output carries only the results.
- An error message names what failed and what to do about it, never a stack trace.
- Run without a terminal (piped, or from a script), the command never waits for input: it takes everything from its arguments, environment or standard input, or fails naming the value it needs.
- Machine-readable output the ticket offers (for example a JSON option) is valid, complete and keeps the same shape on every run.

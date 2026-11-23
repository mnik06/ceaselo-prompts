### Block `library`: a library surface

Every function, type or module the ticket adds or changes in the library's public interface.

- The entry point the ticket names imports without side effects and exposes exactly the public interface the ticket names; internals are not reachable from it.
- Every public function and type is documented where the library documents its interface, with one example of its use.
- Every failure a caller can cause (invalid input, a missing resource, a refused operation) is reported as a typed error naming what failed, never a generic error or a crash.
- Invalid arguments are refused with the typed error naming the argument and the rule it broke, and leave no state changed.

### Live logging

Enable log display during test run (also known as "live logging")

When running tests, `print()` statements and `logging` calls behave differently depending on pytest flags and logger configuration.

| Command / setting                   | `print()` / stdout | `logger.info()` (no logger config) | `logger.warning()` (no logger config) |
|-------------------------------------|--------------------|------------------------------------|---------------------------------------|
| `pytest` (default)                  | captured           | nothing                            | captured (shown on failure)           |
| `pytest -s`                         | live               | nothing                            | nothing (unless failure)              |
| `pytest -o log_cli=true`            | captured           | nothing (level=WARNING)            | live                                  |
| `pytest -s -o log_cli=true`         | live               | nothing (level=WARNING)            | live                                  |
| `pytest --log-cli-level=INFO`       | captured           | **live**                           | live                                  |
| `pytest -svv --log-cli-level=INFO`  | **live**           | **live**                           | live                                  |

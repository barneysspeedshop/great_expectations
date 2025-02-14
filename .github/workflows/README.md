### Great Expectations GitHub Actions

---

* [Auto-Update](autoupdate.yml)
  - Responsible for keeping PR's up-to-date with `develop` (only works if "auto-merge" is turned on)
* [CodeSee Architecture Diagrams](codesee-arch-diagram.yml)
  - Generates a visualization of proposed changes to the codebase through the use of https://www.codesee.io/
* [DataSource Cleanup](data_source_cleanup.yml)
  - Responsible for cleaning up stray schemas left behind from tests
* [StaleBot](stale.yml)
  - Responsible for marking PR's and issues as `stale`
* [PEP-273 Compatability](test-pep273-compatability.yml)
  - Tests for proper zip imports and installation per https://peps.python.org/pep-0273/
* [SQLAlchemy Latest](test-sqlalchemy-latest.yml)
  - Ensures that Great Expectations works with the latest version of SQLAlchemy

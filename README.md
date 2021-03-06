# semgrep-rules

[![r2c community slack](https://img.shields.io/badge/r2c_slack-join-brightgreen?style=for-the-badge&logo=slack&labelColor=4A154B)](https://join.slack.com/t/r2c-community/shared_invite/enQtNjU0NDYzMjAwODY4LWE3NTg1MGNhYTAwMzk5ZGRhMjQ2MzVhNGJiZjI1ZWQ0NjQ2YWI4ZGY3OGViMGJjNzA4ODQ3MjEzOWExNjZlNTA)

| branch | using semgrep docker image | test status          |
| ------------ | ------------------------ | -------------------- |
| `master` | `returntocorp/semgrep:latest`   | [![semgrep-rules-test](https://github.com/returntocorp/semgrep-rules/workflows/semgrep/badge.svg?branch=master)](https://github.com/returntocorp/semgrep-rules/actions?query=workflow%3Asemgrep+branch%3Amaster) |
| `develop` | `returntocorp/semgrep:develop`  | [![semgrep-rules-test-develop](https://github.com/returntocorp/semgrep-rules/workflows/semgrep-develop/badge.svg)](https://github.com/returntocorp/semgrep-rules/actions?query=workflow%3Asemgrep-develop+branch%3Adevelop) |


This is an repository containing rules written for [semgrep](https://semgrep.dev), organized by language. Go to the main semgrep documentation for details on semgrep and the syntax for the yaml files in this repository.

## Security Coverage

`semgrep` features security rules that target [common weaknesses](https://cwe.mitre.org/) and [OWASP categories](https://owasp.org/www-project-top-ten/). Each `security` rule in this repository has metadata fields for `cwe` (and `owasp` when applicable). OWASP coverage for rules in this repository, organized by language, is shown below.

<p align="center">
    <img src="https://web-assets.r2c.dev/semgrep-rules-owasp-coverage-20200520.png" width="500" />
</p>

## Contributing

We welcome contributions to this repo! Please fork and make a pull request; we'll contact you about signing our CLA.

### Rule Namespacing

The namespacing format for contributing rules is `<language>.<framework>.<category>.$MORE`. If a `framework` isn't applicable, use `lang` instead.

`category` is one of:
- security
- correctness
- best-practice
- maintainability
- performance

If a `security` rule is discouraging the use of a bad pattern (such as formatted SQL strings), it is recommended to append `audit` to your namespace. This distinguishes it from a `security` rule that is specifically aiming to detect a vulnerability.

<p align="center">
    <img src="https://web-assets.r2c.dev/semgrep-live-namespacing.png" alt="semgrep.live rule namespace" width="500" />
</p>

## Running Rules in CI/Pre-Commit/Developer Workflow

If you want run these rules rather than write them, check out the easy-to-use [bento.dev](https://bento.dev)

## Help

Join slack for the fastest answers to your questions! Or contact the team at [semgrep@r2c.dev](mailto:semgrep@r2c.dev).

## Testing Rules

A testing system is available which can be used to check the rules against example source code files. It requires `semgrep` from [semgrep](https://semgrep.dev)

If you wrote a rule in a yaml named `eqeq-bad.yaml` with a rule id named `my-eqeq-bad`, you could put a file in the same directory named eqeq-bad.py (it just needs to have the same name except for the extension as eqeq-bad.yaml). Then:

```python
# ruleid:my-eqeq-bad
x == x
```

Running `make test` will execute the test suite, and if `my-eqeq-bad` does not fire on the line below the comment, your rule will fail.

If you have a rule that is not working, but you want to commit it soo it's documented but not fail the tests, use `#todoruleid:...`:

```python
# todoruleid:my-eqeq-bad
x != x
```

### Github Action To Run Tests

If you fork this repo or create your own, you can add a special [semgrep-rules-test](https://github.com/marketplace/actions/semgrep-rules-test) Github Action to your workflow that will automatically test your rules by running `make test` using the latest version of semgrep.

See ours [here](.github/workflows/semgrep-rules-test.yml)


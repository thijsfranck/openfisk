# Contribution Guide

To ensure a smooth collaboration, we have outlined some guidelines to follow when making contributions. Your adherence to these guidelines helps us maintain the quality and clarity of the project.

### Installation

Below are instructions on various ways to install this project. You can choose to either:

1. [Set up a local development environment](#local-installation), or
2. [Use the provided development container](#dev-container-installation) (requires Docker)

#### Local Installation

To develop this project on your local machine, follow the steps outlined below.

> **Note**: Ensure you have Python version 3.12 installed. If not, download it from [here](https://www.python.org/downloads/).

This project uses [Poetry](https://python-poetry.org/) as a dependency manager. Run the following command to install Poetry:

```bash
python -m pip install poetry
```

Next, navigate to the folder where you want the repository to be stored and run the following command to clone the git repository:

```bash
git clone https://github.com/thijsfranck/openfisk
```

Navigate to the root of the repository and run the following command. Poetry will create a virtual environment and install all the necessary dependencies in it.

```bash
poetry install
```

Finally, install the pre-commit hooks for your local repository by running the following command:

```bash
poetry run pre-commit install
poetry run pre-commit install --hook-type commit-msg
```

You're all set! You can now run, develop, build, and test the project in your local development environment.

#### Dev Container Installation

This repository uses the [devcontainers](https://containers.dev) standard to provide a consistent development environment based on a [Docker](https://www.docker.com/) container. To use the devcontainer, please refer to the getting started guide for your IDE:

- [VS Code](https://code.visualstudio.com/docs/devcontainers/containers)
- [IntelliJ IDEA](https://www.jetbrains.com/help/idea/connect-to-devcontainer.html)
- [PyCharm](https://www.jetbrains.com/help/pycharm/connect-to-devcontainer.html)

## Development practices

Please follow the practices and guidelines outline below while developing for this project.

### Tooling

This project uses the following key tools to streamline development:

- Dependency management using [Poetry](https://python-poetry.org/)
- Code linting and formatting using [Ruff](https://github.com/astral-sh/ruff)
- Static type checking using [Pyright](https://github.com/microsoft/pyright)
- Unit testing using [pytest](https://docs.pytest.org)
- Pre-commit hooks using [pre-commit](https://pre-commit.com/)
- A CI/CD environment using [GitHub Actions](https://docs.github.com/en/actions) and [Semantic Release](https://python-semantic-release.readthedocs.io/en/latest/)
- A consistent development environment using a [development container](https://containers.dev)

### Branching

Always create a new branch for your changes. This makes it easier to handle multiple contributions simultaneously.

1. Pull the latest changes from the main branch:

```bash
git pull main
```

2. Create a new branch. Name it descriptively:

```bash
git checkout -b BRANCH_NAME
```

3. Push the branch to the repository:

```bash
git push -u origin BRANCH_NAME
```

### Commit Guidelines

Commit messages should follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) standard. This standard helps us automate the release process and generate changelogs. A conventional commit message should have the following structure:

```text
<type>(optional scope): <description>

[optional body]

[optional footer]
```

The `type` can be one of the following:

- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation changes
- `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `perf`: A code change that improves performance
- `test`: Adding missing tests or correcting existing tests
- `build`: Changes that affect the build system or external dependencies
- `ci`: Changes to our CI configuration files and scripts
- `chore`: Other changes that don't modify src or test files

The `scope` is optional and should describe the section of the codebase that the commit modifies. The `description` should be a short, imperative tense description of the change. The `body` should provide a more detailed description of the change, and the `footer` should contain any issue references.

Here are some examples of conventional commit messages:

```text
fix: correct minor typos in code
feat(my-api): add new feature
```

In case of breaking changes, include the `BREAKING CHANGE` footer with a description of the change, a description of the migration path, and a reference to the issue. For example:

```text
feat: migrate to Python 3.12

BREAKING CHANGE: this change drops support for Python 3.7 and below
```

If you're using the command line to commit, you can use the `commitizen` tool to help you write conventional commit messages. Commitizen is already installed in the development container. To use it, run the following command:

```bash
poetry run cz
```

> **Note**: If you're using VS Code, the development container also automatically installs the `vscode-commitizen` extension, which provides a graphical interface for writing conventional commit messages. It is accessible from the source control panel in the sidebar.

To automatically check your commit messages for compliance with the Conventional Commits standard, you can install a pre-commit hook that checks your commit messages. To install the hook, run the following command:

```bash
poetry run pre-commit install --hook-type commit-msg
```

> **Note**: If you're using the development container, the pre-commit hook is already installed.

### Pull Requests

1. **Creating a Pull Request**: Once you've pushed your branch, navigate to the GitHub repository page and click on the "Pull request" button. Make sure the "base" repository is the main branch and the "compare" branch is the one you've just pushed.

2. **Describe Your Changes**: In the pull request description, explain the changes you've made, any related issues, and provide any additional information or screenshots that might be necessary.

3. **Required Approvals**: Before merging, your pull request must be reviewed and approved by at least one other team member.

4. **Checks**: Ensure that all checks (like CI tests) are passing. If they're not, understand why and make the necessary changes.

### Releases

A new release is automatically created when a commit is pushed to the `master` branch, either directly or through a pull request merge. The release process is automated using GitHub Actions and the `semantic-release` tool. A release includes the following artifacts:

- An archive of the source code (`.tar.gz` and `.zip`)
- Automatically generated release notes

Each release is automatically tagged and published to the GitHub releases page.

#### Versioning

We use [SemVer](https://semver.org/) for versioning. The version number is determined by the type of changes in the commit messages. For example, a commit message with the type `fix` will trigger a patch release, while a commit message with the type `feat` will trigger a minor release. A commit message with the type `BREAKING CHANGE` will trigger a major release.

### Code Documentation

Good code documentation aids understanding and speeds up the development process. For consistency and clarity, we've chosen to use numpy-style docstrings. When documenting your code, please adhere to this style. You can find a complete set of examples in this [style guide](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html).

#### Basic Guidelines

Always document the following elements of your code:

1. **Classes**: including their **attributes and public methods**
2. **Module-level functions and constants**

For classes, functions, and methods, docstrings should start on the line directly below the signature, at the first indent level. For attributes and constants, docstrings should start on the first line after their declaration. Use triple double quotes (`"""`) to enclose your docstrings.

Python type annotations in the function or method signatures are encouraged for clarity. When using type annotations in the signature, it's not necessary to repeat the type in the docstring.

Your docstrings should include these sections in the following order (if applicable):

1. One-line summary
2. Detailed functional description (can span multiple lines, separated by a blank line from the one-line summary)
3. Parameters
4. Returns
5. Raises
6. Examples

For reference, here's a complete example of a function docstring in numpy-style:

```python
def example_function(param1: int, param2: str):
    """One-line summary of the function.

    Detailed functional description of what the function does. Can span
    multiple lines.

    Parameters
    ----------
    param1 : int
        Description of the first parameter.
    param2 : str
        Description of the second parameter.

    Returns
    -------
    bool
        Description of the return value.

    Raises
    ------
    ValueError
        Description of the error.

    Examples
    --------
    >>> example_function(1, "test")
    True
    """
    return True
```

For classes and attributes:

```python
class Example:
    """Class-level docstring describing the class."""

    attribute: int
    """Description of the class attribute."""
```

Prioritize documenting public methods and attributes (those not starting with an underscore). However, private methods with complex logic should also be documented for clarity.

### Unit Testing

Unit tests are key to our success, since they allow us to catch bugs early, run sections of code in isolation, and accelerate our development pace. We use the `pytest` framework for writing and running our tests.

#### Basic Guidelines

Test modules should be located in the same directory as the module they cover. Test modules should be named `test__*.py` (e.g.,` test__math_ops.py`). Individual test methods within those modules should be prefixed with `test__` (e.g., `test__my_function`). See the example below:

```text
project_root/
├── utils/
│   ├── __init__.py
│   ├── math_ops.py
│   └── test__math_ops.py
├── main.py
└── ...
```

As a general rule, unit tests should cover the following aspects of your code:

- Input validation
- Validation of output (or outcome) given a particular input
- Error handling

The `examples` folder includes [sample tests](./examples/test__example.py) that you can use as a base for your own test.

#### Unit Testing and Type Hints

You can reduce the need for unit tests by indicating the expected types of input arguments and return values as type hints. While they don't replace unit tests, type hints can reduce the number of tests you might need to write, particularly those related to input validation.

For instance, consider the following function without type hints:

```python
def add(a, b):
    return a + b
```

Without type hints, you might write multiple tests to ensure that the function behaves correctly with different types of input, like strings, integers, or floats. But with type hints:

```python
def add(a: int, b: int) -> int:
    return a + b
```

The function's expected behavior is clearer. You know that both `a` and `b` should be integers, and the return value will also be an integer. With these type hints in place, there's less need to write unit tests checking for behaviors with non-integer inputs since the static type checker can catch those mistakes for you.

#### Writing Tests

1. **Import Dependencies**: Start by importing `pytest` and the module, class, or function you're testing.
2. **Create Test Cases**: Each test case should have its own test function with a descriptive name.
3. **Setup and Teardown**: Use `pytest` fixtures to define startup and teardown routines.

#### Running Tests

To run the tests, use the following command from the root of the project:

```bash
poetry run pytest
```

This command will discover and run all the tests that match the pattern `test__*.py`.

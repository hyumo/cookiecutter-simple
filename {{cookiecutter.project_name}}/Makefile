.PHONY: install
install: ## Install the poetry environment and install the pre-commit hooks
	@echo "🚀 Creating virtual environment and install dependencies"
	@python3 -m venv .venv
	@. .venv/bin/activate
	@pip install -r requirements-dev.txt

.PHONY: check
check: ## Run code quality tools.
	@echo "🚀 Linting code: Running ruff"
	@ruff check . --force-exclude
	@echo "🚀 Static type checking: Running mypy"
	@mypy .
	@echo "🚀 Autoformat: Running black"
	@black .
{%- if cookiecutter.deptry == 'y' %}
	@echo "🚀 Checking for obsolete dependencies: Running deptry"
	@deptry .
{%- endif %}

.PHONY: test
test: ## Test the code with pytest
	@echo "🚀 Testing code: Running pytest"
	@run pytest --cov --cov-config=pyproject.toml --cov-report=xml
	@run pytest --doctest-modules

.PHONY: build
build: clean-build ## Build wheel file using poetry
	@echo "🚀 Creating wheel file"
	@echo "WIP"

.PHONY: clean-build
clean-build: ## clean build artifacts
	@rm -rf dist

# .PHONY: publish
# publish: ## publish a release to pypi.
# 	@echo "🚀 Publishing: Dry run."
# 	@poetry config pypi-token.pypi $(PYPI_TOKEN)
# 	@poetry publish --dry-run
# 	@echo "🚀 Publishing."
# 	@poetry publish

# .PHONY: build-and-publish
# build-and-publish: build publish ## Build and publish.

{%- if cookiecutter.mkdocs == "y" %}

.PHONY: docs-test
docs-test: ## Test if documentation can be built without warnings or errors
	@mkdocs build -s

.PHONY: docs
docs: ## Build and serve the documentation
	@mkdocs serve

{%- endif %}

.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'

.DEFAULT_GOAL := help
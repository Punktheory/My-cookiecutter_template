.PHONY: help test lint format

help:
@echo "Available targets: test, lint, format"

test:
pytest -q

lint:
ruff check .

format:
ruff format .

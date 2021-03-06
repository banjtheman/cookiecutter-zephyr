# -----------------------------------------------------------------------------
# Makefile for {{cookiecutter.app_name}}
#
# Commands:
# help                        Print help documentation
# black                       Run Python's Black formatter on the code
# build_image                 Build the Docker Images
# build_package               Build the Python Package (using setuptools)
# clean                       Clean Python Package Data (Tests/Eggs/Cache)
# install                     Install the python package locally for testing
# mypy                        Run Python's Mypy type checker on the code
# pylint                      Run Python's Pylint syntax checker on the code
# test                        Test the python package (using setuptools and pytest)
# test_unit                   Run Unit Tests (using setuptools and pytest
# todo                        Get project TODOs
#
# Example Call:
#    make build_image
# -----------------------------------------------------------------------------


###
# Variables
###


VERSION=`cat ./VERSION`


###
# Help/Setup
###


# Make phone commands
.PHONY: test build install clean todo

help:
	# Print help documentation
	@echo "This makefile holds the following targets"
	@echo "  help                        Print help documentation"
	@echo "  black                       Run Python's Black formatter on the code"
	@echo "  build_image                 Build the Docker Images"
	@echo "  build_package               Build the Python Package (using setuptools)"
	@echo "  clean                       Clean Python Package Data (Tests/Eggs/Cache)"
	@echo "  install                     Install the python package locally for testing"
	@echo "  mypy                        Run Python's Mypy type checker on the code"
	@echo "  pycodestyle                 Run Pycodestyle on the package"
	@echo "  pylint                      Run Python's Pylint syntax checker on the code"
	@echo "  test                        Test the python package (using setuptools and pytest)"
	@echo "  test_unit                   Run Unit Tests (using setuptools and pytest)"
	@echo "  todo                        Get project TODOs"


###
# Development/Standards Tools
###


todo:
	# Get all package TODOs
	grep -rE "TODO" | egrep .py | egrep -v .html | egrep -v .eggs | egrep -v .pyc

mypy:
	# Run Mypi on the package
	python3 -m mypy --config-file=.mypy.ini

pycodestyle:
	# Run Pycodestyle on the package
	python3 -m pycodestyle --config=.pycodestylerc

pylint:
	# Run Pylint on the package
	python3 scripts/run_pylint.py --min-score=7.5

black:
	# Run Black on the package
	python3 -m black --config=.blackrc.toml


###
# Test Steps
###


test: test_unit
	# Run all test steps

test_unit:
	# Run Unit Tests (using setuptools and pytest)
	python3 setup.py test


###
# Buid Process
###


build_package:
	# Build the Python Package (using setuptools)
	pip install --editable .

build_image:
	# Build the Docker Image
	docker-compose build


###
# Cleanup Process
###


clean:
	# Clean Python Package Data (Tests/Eggs/Cache)
	rm -rf \
		*.DS_Store* \
		*.egg* \
		.eggs \
		.pytest_cache/ \
		.mypy_cache/ \
		reports/ \
		.coverage \
		build/
	find . -name '__pycache__' -type d | xargs rm -fr
	find . -name '*.pyc' -delete
	find . -name '*.pyo' -delete

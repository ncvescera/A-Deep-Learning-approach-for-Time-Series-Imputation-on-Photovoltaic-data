SHELL:=/bin/bash
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := latexmk
DOCUMENT := main.tex
ZIPARCHIVE_THESIS := A-Deep-Learning-approach-for-Time-Series-Imputation-on-Photovoltaic-data.zip
ZIPARCHIVE_PRESENTATION := presentazione_tesi.zip
FORMATTER := latexindent
LINTER := chktex
LINTER_IGNORE := -n 8 -n 1
DIR_THESIS := thesis
DIR_PRESENTATION := presentation

# .PHONY: build
all: extract start format build clean stop

start:
	docker container start $(CONTAINER)

stop:
	docker container stop $(CONTAINER)

install:
	docker exec -it $(CONTAINER) tlmgr install `cat requirements.txt` && texhash

thesis: extract-thesis start format build-thesis clean stop

presentation: extract-presentation start format build-presentation clean stop

build-thesis: start
	docker exec -it $(CONTAINER) cd $(DIR_THESIS) && $(LATEXCOMPILER) -pdf -shell-escape -synctex=1 --enable-write18 -interaction=nonstopmode $(DOCUMENT)

build-presentation: start
	docker exec -it $(CONTAINER) $(LATEXCOMPILER) -pdf -shell-escape -synctex=1 --enable-write18 -interaction=nonstopmode $(DIR_PRESENTATION)/$(DOCUMENT)

extract-thesis: $(DIR_THESIS)/$(ZIPARCHIVE_THESIS)
	unzip -o $^ -d $(DIR_THESIS)
	rm $^

extract-presentation: $(ZIPARCHIVE_PRESENTATION)
	unzip -o $(ZIPARCHIVE_PRESENTATION)
	rm $(ZIPARCHIVE_PRESENTATION)

check-thesis: start
	docker exec -it $(CONTAINER) $(LINTER) $(LINTER_IGNORE) $(DIR_THESIS)/$(DOCUMENT)

check-presentation: start
	docker exec -it $(CONTAINER) $(LINTER) $(LINTER_IGNORE) $(DIR_PRESENTATION)/$(DOCUMENT)

format: start
	docker exec -it $(CONTAINER) $(FORMATTER) -w $(shell find . -name "*.tex")

clean:
	docker exec -it $(CONTAINER) latexmk -c
	find . -name "*.aux" | xargs rm
	find . -name "*.log" | xargs rm
	find . -name "*.toc" | xargs rm
	find . -name "*.out" | xargs rm
	find . -name "*.gnuplot" | xargs rm
	find . -name "*.xml" | xargs rm
	find . -name "*.bak*" | xargs rm


help:
	@echo "Makfile Help:"
	@echo "	usage: make <target> [VAR=value]"
	@echo ""
	@echo "	targers:"
	@echo "		- start: Starts the devcontainer for LaTex environment."
	@echo "		- stop: Stops the devcontainer"
	@echo "		- build: Starts the devcontainer first, then execute the build process using the devcontainer."
	@echo "		         Can set the following variables:"
	@echo "		            - CONTAINER: docker container name to be used."
	@echo "		            - LATEXCOMPILER: latex compiler to be used. Some compilers are: latexmk, pdftex, lualatex, ..."
	@echo "		            - DOCUMENT: main document file."
	@echo "		- format: Starts the devcontainer first, then execute the formatting progecc."
	@echo "		          Can set the following variables:"
	@echo "		             - CONTAINER: docker container name to be used."
	@echo "		             - FORMATTER: LaTex formatter to be used."
	@echo "		- extract: Extract the .zip file from Overleaf."
	@echo "		           Can set the following variables:"
	@echo "		              - ZIPARCHIVE: zip file name."
	@echo "		- clean: Removes all temporary files."
	@echo "		         Can set the following variables:"
	@echo "		            - CONTAINER: docker container name to be used."
	@echo "		- check: Starts the developer container first, then runs the LaTex Linter."
	@echo "		         Can set the following variables:"
	@echo "		            - CONTAINER: docker container name to be used."
	@echo "		            - LINTER: LaTex linter. 'chktex' is the default one."
	@echo "		            - DOCUMENT: main document file."
	@echo "		- install: Install LaTex packages found inside 'requirements.txt' file"
	@echo "		- all: Runs extract, start, format, build and clean targets (in this order)."
	@echo "		       Can be invoked just with 'make'."

SHELL:=/bin/bash
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := latexmk
DOCUMENT := main.tex
ZIPARCHIVE := A-Deep-Learning-approach-for-Time-Series-Imputation-on-Photovoltaic-data.zip
FORMATTER := latexindent
LINTER := chktex

# .PHONY: build
all: extract start check format build clean stop

start:
	docker container start $(CONTAINER)

stop:
	docker container stop $(CONTAINER)

build: start
	docker exec -it $(CONTAINER) $(LATEXCOMPILER) -pdf -shell-escape -synctex=1 --enable-write18 -interaction=nonstopmode $(DOCUMENT)
	# $(MAKE) stop

format: start
	docker exec -it $(CONTAINER) $(FORMATTER) -w $(shell find . -name "*.tex")

extract: $(ZIPARCHIVE)
	unzip -o $(ZIPARCHIVE)
	rm $(ZIPARCHIVE)

clean:
	docker exec -it $(CONTAINER) latexmk -c
	find . -name "*.aux" | xargs rm
	find . -name "*.log" | xargs rm
	find . -name "*.toc" | xargs rm
	find . -name "*.out" | xargs rm
	find . -name "*.gnuplot" | xargs rm
	find . -name "*.xml" | xargs rm
	find . -name "*.bak*" | xargs rm

check: start
	docker exec -it $(CONTAINER) $(LINTER) $(DOCUMENT)


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
	@echo "		- check:"

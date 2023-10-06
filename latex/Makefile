SHELL:=/bin/bash
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := latexmk
DOCUMENT := main.tex
ZIPARCHIVE := A-Deep-Learning-approach-for-Time-Series-Imputation-on-Photovoltaic-data.zip
FORMATTER := latexindent

# .PHONY: build
all: extract start format build clean stop

start:
	docker container start $(CONTAINER)

stop:
	docker container stop $(CONTAINER)

build: start
	docker exec -it $(CONTAINER) $(LATEXCOMPILER) -pdf -shell-escape -synctex=1 --enable-write18 -interaction=nonstopmode $(DOCUMENT)
	# $(MAKE) stop

format: start
	docker exec -it $(CONTAINER) latexindent -w $(shell find . -name "*.tex")

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


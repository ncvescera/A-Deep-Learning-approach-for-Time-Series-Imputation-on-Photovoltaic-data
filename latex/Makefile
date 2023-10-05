
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := pdflatex
DOCUMENT := main.tex
ZIPARCHIVE := A-Deep-Learning-approach-for-Time-Series-Imputation-on-Photovoltaic-data.zip

# .PHONY: build

start:
	docker container start $(CONTAINER)

build: start
	docker exec -it $(CONTAINER) $(LATEXCOMPILER) -pdf -shell-escape -synctex=1 --enable-write18 -interaction=nonstopmode $(DOCUMENT)

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


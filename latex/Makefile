
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := lualatex
DOCUMENT := main.tex
ZIPARCHIVE := A-Deep-Learning-approach-for-Time-Series-Imputation-on-Photovoltaic-data.zip

# .PHONY: build

start:
	docker container start $(CONTAINER)

build: start
	 docker exec -it $(CONTAINER) $(LATEXCOMPILER) $(DOCUMENT)

extract: $(ZIPARCHIVE)
	unzip -o $(ZIPARCHIVE)
	rm $(ZIPARCHIVE)

clean:
	find . -name "*.aux" | xargs rm
	find . -name "*.log" | xargs rm
	find . -name "*.toc" | xargs rm
	find . -name "*.out" | xargs rm
	find . -name "*.gnuplot" | xargs rm
	find . -name "*.xml" | xargs rm


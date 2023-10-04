
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


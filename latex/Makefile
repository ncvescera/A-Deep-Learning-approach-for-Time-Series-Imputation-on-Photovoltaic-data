
CONTAINER := latex_devcontainer-vscode-1
LATEXCOMPILER := lualatex
DOCUMENT := main.tex

.PHONY: build

start:
	docker container start $(CONTAINER)

build: start
	 docker exec -it $(CONTAINER) $(LATEXCOMPILER) $(DOCUMENT)

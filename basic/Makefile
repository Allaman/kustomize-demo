.PHONY: help
help: ## This help.
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)
.DEFAULT_GOAL := help

BUILD:=kustomize build

build-dev: req-kustomize ## Generate develop manifests - do not apply them
	@mkdir -p generated
	@$(BUILD) overlay/dev > generated/dev.yml
build-test: req-kustomize ## Generate test manifests - do not apply them
	@mkdir -p generated
	@$(BUILD) overlay/test > generated/test.yml
build-prod: req-kustomize ## Generate production manifests - do not apply them
	@mkdir -p generated
	@$(BUILD) overlay/prod > generated/prod.yml

build-all: req-kustomize build-dev build-test build-prod ## Generate all manifests - do not apply them

req-kustomize:
	@command -v kustomize >/dev/null 2>&1 || { echo >&2 "require kustomize"; exit 1; }

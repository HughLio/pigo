ifeq ($(OS),Windows_NT)
    BROWSER = start
else
	UNAME := $(shell uname -s)
	ifeq ($(UNAME), Linux)
		BROWSER = xdg-open
	endif
	ifeq ($(UNAME), Darwin)
		BROWSER = open
	endif
endif

.PHONY: all clean serve

all: wasm serve

demo: masquerade serve

wasm:
	cp -f "$$(go env GOROOT)/misc/wasm/wasm_exec.js" ./js/
	GOOS=js GOARCH=wasm go build -o lib.wasm wasm.go

masquerade:
	cp -f "$$(go env GOROOT)/misc/wasm/wasm_exec.js" ./js/
	GOOS=js GOARCH=wasm go build -o lib.wasm demo.go

serve:
	$(BROWSER) 'http://localhost:5000'
	serve

clean:
	rm -f *.wasm

debug:
	@echo $(UNAME)

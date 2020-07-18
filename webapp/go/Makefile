export GO111MODULE=on

all: isucari

isucari: *.go
	GOOS=linux go build -o isucari

.PHONY: deploy
deploy: isucari
	scp ./isucari isucon9-001:/home/isucon/isucari/webapp/go/isucari

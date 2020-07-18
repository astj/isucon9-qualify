export GO111MODULE=on

all: isucari

isucari: *.go
	GOOS=linux go build -o isucari

.PHONY: deploy
deploy: isucari
	ssh isucon9-001 'sudo systemctl stop isucari.golang.service'
	scp ./isucari isucon9-001:/home/isucon/isucari/webapp/go/isucari
	ssh isucon9-001 'sudo systemctl start isucari.golang.service'

.PHONY: initialize
initialize:
	scp ./initialize.json isucon9-001:/home/isucon/isucari/webapp/
	ssh isucon9-001 'curl -XPOST http://127.0.0.1:8000/initialize -H "Content-Type: application/json" -d @/home/isucon/isucari/webapp/initialize.json'

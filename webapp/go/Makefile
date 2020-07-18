export GO111MODULE=on

all: isucari

isucari: *.go
	GOOS=linux go build -o isucari

.PHONY: deploy
deploy: isucari
	ssh isucon9-001 'sudo systemctl stop isucari.golang.service'
	scp ./isucari isucon9-001:/home/isucon/isucari/webapp/go/isucari
	ssh isucon9-001 'sudo systemctl start isucari.golang.service'
	ssh isucon9-003 'sudo systemctl stop isucari.golang.service'
	scp ./isucari isucon9-003:/home/isucon/isucari/webapp/go/isucari
	ssh isucon9-003 'sudo systemctl start isucari.golang.service'

.PHONY: restart
restart:
	ssh isucon9-001 'sudo systemctl restart isucari.golang.service'
	ssh isucon9-003 'sudo systemctl restart isucari.golang.service'

.PHONY: initialize
initialize:
	scp ./initialize.json isucon9-001:/home/isucon/isucari/webapp/
	ssh isucon9-001 'curl -XPOST http://127.0.0.1:8000/initialize -H "Content-Type: application/json" -d @/home/isucon/isucari/webapp/initialize.json'

.PHONY: bench
bench:
	ssh isucon9-001 "echo '' > /var/log/nginx/isucari-access.log"
	ssh isucon9-002 "echo '' > /var/log/mysql/slow.log"
	ssh isucon9-bench 'cd /home/isucon/isucari && ./bin/benchmarker -payment-port 5556 -payment-url http://isucon9-bench:5556/ -shipment-port 7001 -shipment-url http://isucon9-bench:7001/ -target-url http://isucon9-001:8001/'

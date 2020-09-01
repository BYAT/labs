pro-graf: pro-graf-clone pro-graf-up pro-graf-test pro-graf-tidy

pro-graf-clone:
	git clone https://github.com/Danya-Mudaifea/pro-graf

pro-graf-up:
	cd pro-graf && ./pro-graf.sh

pro-graf-test:
	curl localhost/grafana

pro-graf-tidy:
	rm -rf pro-graf

pro-graf-down:
	helm uninstall prometheus-operator -n monitor


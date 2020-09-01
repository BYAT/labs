elf: elf-clone elf-up elf-test elf-tidy

elf-clone:
	git clone https://github.com/Danya-Mudaifea/elf

elf-up:
	cd elf && ./elf.sh

elf-test:
	curl localhost/elf

elf-tidy:
	rm -rf elf

elf-down:
	helm uninstall elasticsearch --namespace=elf
	helm uninstall fluent-bit --namespace=elf
	helm uninstall kibana --namespace=elf
	kubectl delete random-logger -n elf
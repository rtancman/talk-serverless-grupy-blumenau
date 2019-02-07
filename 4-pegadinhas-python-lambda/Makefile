lambda.docker.build:
	@echo "---- Create amazon linux image base ----"
	@docker build -t amazon-linux-python37 .

lambda.docker.pkgcreate:
	@echo "---- Create Lambda Package using amazon linux image base ----"
	@docker run --rm -u `id -u` \
    -v ~/.aws/:/home/lambda/.aws/ \
    -v `pwd`:/app \
		-e "HOME=/home/lambda" \
		amazon-linux-python37 pip3.7 install -r requirements.txt -t .
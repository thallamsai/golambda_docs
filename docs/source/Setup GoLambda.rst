Setup GoLambda
====================================

We will setup Golambda in docker container. This way it will help in test in local and pp.

Pre-requisite
^^^^^^^^^^^^^

* Install docker
* Install docker-compose
* Setup AWS cli

Install Docker 3
^^^^^^^^^^^^^^^^

* `Mac <https://docs.docker.com/docker-for-mac/install/>`_
* `Ubuntu <https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/>`_
* `Windows <https://docs.docker.com/docker-for-windows/install/>`_

Install docker-compose
^^^^^^^^^^^^^^^^^^^^^^

* `docker-compose <https://docs.docker.com/compose/install/>`_

Setup AWS CLI
^^^^^^^^^^^^^

* `AWS Cli <https://docs.aws.amazon.com/cli/latest/userguide/installing.html>`_

Configure AWS CLI
^^^^^^^^^^^^^^^^^

* run  `aws configure`
* Access key ID: `AKIAIHXF4V7CQA3YILRA`
* Secret access key: `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`
* After configuration run `$(aws ecr get-login --no-include-email --region ap-south-1)` 

Start Development
^^^^^^^^^^^^^^^^^

* Download `docker-compose.yml`  and `Dockerfile-Dev` in the root directory of Lambda project
* run `docker-compose build` and then `docker-compose up`
* To initialise app: run `docker-compose exec golambda_vertical python generator.py init`
* To add a new Action: run `docker-compose exec golambda_vertical python generator.py addAction`

Test your Setup
^^^^^^^^^^^^^^^
..  http:example:: curl

	POST /api/action_handler/ HTTP/1.1
    Host: localhost:8081
    Accept: application/json
    Content-Type: application/json
    Authorization: Basic YWRtaW46YWRtaW4=

    {
	    "subIntent": "default",
	    "intent": "<Your intent>",
	    "context": {
				"email": "<any valid email>",
		        "mobile": "<any valid phone number>"
		        }
	}

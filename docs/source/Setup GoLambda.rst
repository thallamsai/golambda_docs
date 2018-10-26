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

* run  ``aws configure``
* Access key ID: <>
* Secret access key: <>
* After configuration run ``$(aws ecr get-login --no-include-email --region ap-south-1)``

Please refer diana_lambda readme file for credentials. 

Start Development - New Vertical and New Intent
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Clone the repo ``https://github.com/goibibo/golambda_vertical.git``
* Your golambda project structure should be as below: 
* run ``docker-compose build`` and then ``docker-compose up``
* To initialise app: run ``docker-compose exec golambda_vertical python generator.py init``

* To add a new Action: run ``docker-compose exec golambda_vertical python generator.py addAction``
* - Domain = goibibo , Vertical = train
* Copy from above repo `docker-compose.yml`  and `Dockerfile-Dev` in to the root directory of your Lambda project.

Steps to migrate from Diana lambda to Golambda 2.0
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
After completing above steps mentioned in **Start Development - New Vertical and New Intent** please follow below steps

* Create directories <domain>/<vertical> like goibibo/train
* Copy all your vertical related py files to <domain>/<vertical>
* Copy contents of your config.py to config.py in root folder.
* Create constants.py file in root folder. 
* In config.py, append your folder path in OWNER_LIST, for eg. goibibo flights team will write ``OWNER_LIST = ["goibibo.flight"]`` 
* In config.py file add your docker url like ``LAMBDA_URL = 'http://gia-train.goibibo.com' if settings.ENV_TYPE == 'prod' else 'http://0.0.0.0:8001'``
* Copy your message files to message_yaml
* Wherever there are references to constants and confing in your code, change import statment as ``from vertical.constants import DB_BOOKING_STATUS``
* Replace ``golambda.goibibo`` to ``vertical.goibibo`` and ``golambda.makemytrip`` to ``vertical.makemytrip`` in all your py files. 



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

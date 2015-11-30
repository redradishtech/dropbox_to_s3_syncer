# Docker Dropbox-to-Amazon-S3 Syncer

## Installation

On Ubuntu:

1. First [install docker](http://docs.docker.com/v1.8/installation/ubuntulinux/) and [install docker compose](https://docs.docker.com/compose/install/).

2. Copy `.env.sample` to `.env`, and customize with the AWS credentials, S3 bucket and other details.

3. Get the required Docker build files:

	git clone https://github.com/redradishtech/docker-dropbox_to_s3_syncer.git
	git clone https://github.com/redradishtech/docker-dropbox.git

4. Run `docker-compose up dropbox`. You should see repeated messages of the form:

    dropbox_1 | This computer isn't linked to any Dropbox account...
    dropbox_1 | Please visit https://www.dropbox.com/cli_link_nonce?nonce=xxxxxxxxxxxxxxxxxxxxxxxxx to link this device.

5. Visit the URL to authorize the Dropbox instance, after which the docker log should report:

    dropbox_1 | This computer is now linked to Dropbox. Welcome <name>

To check on the sync status, run:

    docker exec -it dropbox dropbox status

Once this returns 'Up to date', your ./dropbox/Dropbox directory should mirror your Dropbox content.

6. Now run `docker-compose up s3syncer`. If you set the variables correctly in `.env`, 

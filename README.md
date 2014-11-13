# UnveillanceDeploy

This is a handy utility to build Docker containers dedicated to your Unveillance Annexes.  Simply add your Annex project into the root folder, and either run `./build_image.sh` and follow the prompts; or use `./build_image.sh /path/to/custom/config.json` after creating your own config.

## Setup

`./setup.py`

## Adding an Annex project

1.	`cd UnveillanceDeploy`
1.	`cp /your/Annex/Package .` or `git clone git@host:your/AnnexPackage.git`
1.	if you cloned, you will also have to `git submodule update --init --recursive` 

## Configuration

You can create a config.json file with the following format:

	{
		"secrets": {
			"uv_server_host": "localhost",				# what the Annex will report as its hostname
			"uv_uuid": "my_annex",						# the Annex's short-code or nickname
			"annex_dir": "/home/unveillance/annex"		# where the Annex should store its files
		},
		"nginx": {
			"client_max_body_size": 10, 				# in MB, should you require uploads into the Annex from a Frontend client
			"proxy_main_port": 8889						# the port the Annex will serve its API out of
		}, 
		"docker": {
			"SUPER_PACKAGE": "CompassAnnex", 			# the name of the package you wish to deploy
			"ANNEX_USER": "unveillance", 				# unix user
			"ANNEX_USER_PWD" : "ohmigerd",				# user's password.  you should remember it, but it's not too important because sudoer
			"EXTRA_PORTS": "8887",						# if you require extra ports to be opened, list them here: space-separated string
			"ssh_root": "/home/unveillance/.ssh"		# where we'll put the Annex user's .ssh
		}
	}

If any of these directives are missing, you will be prompted during the build process.

## Deploy

Your Docker image is now available and can be deployed at any time via Docker using `sudo docker run -i -t compassannex:unveillance` (or whatever the image turns out to be named, given your inputs).
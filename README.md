# Weatherapp

Simple web app with the purpose of displaying current weather in configured location.

Cloud instance has been deployed on Azure and can be found at https://weatherapp-front.azurewebsites.net/

## Running the app 

### In containers

The easiest way to run the app is by using [docker compose](https://docs.docker.com/compose/). First you need to create **.env** files in **frontend** and **backend** directories. Then copy the contents of **.env.sample** files in their respective directories to newly created **.env** files, fill in missing values and replace or add other configuration properties if neccessary (refer to [Environmental properties](#environmental-properties) for more details).
After environment has been set, execute `docker-compose up` in root directory of the project to start the containers.

Alternatively if you want to separately build and run the container run `docker build -t your_container_name path_to_directory_with_dockerfile` to build the container and `docker run -t your_container_name` to run it.

### Locally

To run the app locally you need [nodejs](https://nodejs.org/). Both backend and frontend can be run by executing `npm i && npm start` in their respective directories. Neccessary environmental properties still need to be set.

## Environmental properties

### Backend

| Property     | Description                                                                 | Default value                          |
|--------------|-----------------------------------------------------------------------------|----------------------------------------|
| APPID        | Aplication key for [openweathermap](http://openweathermap.org/)             |                                        |
| PORT         | TCP port on which the app will listen                                       | 9000                                   |
| MAP_ENDPOINT | Base URL for weathermap API calls                                           | http://api.openweathermap.org/data/2.5 |
| TARGET_CITY  | City parameter for weathermap API calls                                     | Helsinki,fi                            |

### Frontend

| Property     | Description                                                                 | Default value                          |
|--------------|-----------------------------------------------------------------------------|----------------------------------------|
| ENDPOINT     | Base URL for backend API calls                                              | http://0.0.0.0:9000/api                |
| PORT         | TCP port on which the app will listen                                       | 8000                                   |

## Installing app using Ansible

This repository includes [Ansible](https://www.ansible.com/) playbook that can install docker and the app on specified hosts, to create ready to deploy package.

To run the palybook execute `ansible-playbook ./ansible/install.yml -i selected_inventory_file`. Currently 2 inventory files are provided: **ansible/local.ini** and **ansible/cloud.ini**(incomplete). **.env** files can be created either before the playbook is executed so they are automatically copied to cloned repository or after, directly in the clone. If those files are not in their default locations you must declare `front_env_file` and `back_env_file` variables for ansible. Another configurable parameter is `repo_clone_dir` which specifies direcotry path which will become the cloned app repository. To pass those variables you could for example fill them in in **ansible/vars-sample.yml** file and add `--extra-vars @ansible/vars-sample.yml` option to ansible command. For more details refer to [Ansible documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html).


## Would be nice to have / not finished

- Fix issues with Azure Application Gateway. You should be able to access the app via reverse proxy at [20.215.88.100](http://20.215.88.100/), but currently it returns 404 status code.

- Expose cloud instance via ssh. With the way app was deployed (Azure App Service) this may prove troublesome, since App Service allows only one port to be exposed to the ouside world. For this reason it might be neccessary to redeploy the app using another Azure feature.

- It would make more sense to store ansible related files in another repository, so they are not confused with something neccessary for the app and not downloaded by the playbook, but for the sake of keeping this exersice in a single repo this was not done.

- Configure cloud inventory for ansible once the cloud instance is available via ssh.

- Create Terraform configuration.

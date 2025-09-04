####################################################################################################################
# Setup containers to run Airflow

# This command builds the docker images, initializes the Airflow DB, and starts the services in detached mode.
docker-spin-up:
	docker compose build && docker compose up airflow-init && docker compose up --build -d

# This command creates the necessary local directories and sets the correct permissions.
# It references the dbt_project directory now.
perms:
	mkdir -p logs plugins dags tests && chmod -R 777 logs plugins dags tests dbt_project

# A simple sleep command to allow services time to initialize.
do-sleep:
	sleep 30

# Main command to bring up the environment.
up: perms docker-spin-up do-sleep

# Command to stop and remove all containers defined in the docker-compose file.
down:
	docker compose down

# A convenient command to restart the entire environment.
restart: down up

# Command to get a bash shell inside the running scheduler container for debugging.
sh:
	docker exec -ti scheduler bash

# Command to generate and serve the dbt documentation.
# The path has been updated to dbt_project.
dbt-docs:
	docker exec -d webserver bash -c "cd /opt/airflow/dbt_project && dbt docs serve --host 0.0.0.0 --port 8081"

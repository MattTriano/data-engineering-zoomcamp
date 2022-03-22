# Workflow Orchestration (Airflow)

The official airflow quick setup instructions: Run the following commands to download the `docker-compose` app, set up the 


```bash
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.2.4/docker-compose.yaml'
mkdir -p ./dags ./logs ./plugins
echo -e "AIRFLOW_UID=$(id -u)" > .env
docker-compose up airflow-init
```

and then you can start up up the airflow docker-compose as you normally would.

```bash
docker-compose up
``` 
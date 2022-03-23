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

I'm writing these things locally then using `sftp` to `put` things on my GCP VM. `sftp` can move files easily, but if a directory doesn't exist yet, it will complain when you try to put it up, so you have to make the top-level directories first (but then you can use the `-r` flag to recursively put up subdirectories). 


```bash
sftp> mkdir ./dags
sftp> mkdir ./logs
sftp> mkdir ./plugins
sftp> put -r ./dags
sftp> put -r ./logs
sftp> put -r ./plugins
```

The official docker-compose app will work as a stand-alone application, but we'll have to adapt it to work with our google cloud vm. We'll need to write a Dockerfile that installs the gcloud sdk, fortunately the Airflow documentation contains a mostly complete example (although it's getting a bit stale, as it's for google sdk v322.0 but the most current version is v349.0.

https://github.com/apache/airflow/blob/main/docs/docker-stack/docker-images-recipes/gcloud.Dockerfile

Also, the zoomcamp instructors added a line to slip `vim` into the Dockerfile, but I don't know why they'd put that in there. It's high up in the dockerfile, so removing it would cause a lot to have to recompile, but I just don't think I'll need `vim`. 

I would like to leave some bits of information out of my github repo, so I'm going to stow some secrets in environment variables and adapt the docker-compose file to look for them there.


## Port Forwarding

I modified my `~/.ssh/config` file to automatically port forward while also providing an ssh connection.

```bash
Host dtc-*
	HostName <VM_external_IP_addr>
	User <user>
	IdentityFile <location_of_ssh_private_key>

Host dtc-de-zoomcamp
	TCPKeepalive Yes

Host dtc-airflow_webserver
	LocalForward <my_local_machine_port> localhost:<port_on_vm>
```

Which allows me to access the airflow webserver at url `http://localhost:<my_local_machine_port>/home`
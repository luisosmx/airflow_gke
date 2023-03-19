# airflow_gke

# Para acceder a airflow mediante gke, es necesario tener creado un PROJECTO en gcp y despues ejecutamos los siguientes comandos en la CLOUD SHELL de gcp

$ gcloud container clusters create airflow-cluster --machine-type n1-standard-4 --num-nodes 1 --region "us-central1-a"

$ gcloud container clusters get-credentials airflow-cluster --region "us-central1-a"

$ kubectl create namespace airflow

$ helm repo add apache-airflow https://airflow.apache.org

$ helm repo list

$ helm upgrade --install airflow apache-airflow/airflow -n airflow --debug

$ kubectl port-forward svc/airflow-webserver 8080:8080 -n airflow

# Una vez que ejecutamos el ultimo comando nos dirijimos a la pagina de gcp y buscamos el cluster airflow-webserver
![image](https://user-images.githubusercontent.com/119461863/226150908-5164160b-1699-4ba8-8d71-7318918f10e8.png)

# Damos clic en ese cluster y buscamos la siguiente ventana 

![image](https://user-images.githubusercontent.com/119461863/226150985-f09c2508-9e81-4230-898b-c525400fd452.png)

# Al dar clic nos abrira una ventana que contiene un comando, lo copiamos y lo ejecutamos en la terminal de wsl

![image](https://user-images.githubusercontent.com/119461863/226151117-0f5f309e-2b50-4005-b9aa-934b01cc270e.png)

# Una vez ejecutado ese comando nos dara una direccion como la de la imagen, la copiamos y la ejecutamos en una nueva ventana 

![image](https://user-images.githubusercontent.com/119461863/226151316-d3e27213-02dd-473b-807b-e96a751f25c6.png)



Paginas consultadas: https://towardsdatascience.com/deploying-airflow-on-google-kubernetes-engine-with-helm-28c3d9f7a26b 

https://chat.openai.com/chat


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

# Al dar clic nos abrira una ventana que contiene un comando, lo copiamos y lo ejecutamos en la terminal de wsl en vsc

![image](https://user-images.githubusercontent.com/119461863/226151117-0f5f309e-2b50-4005-b9aa-934b01cc270e.png)

# Una vez ejecutado ese comando nos dara una direccion como la de la imagen, la copiamos y la ejecutamos en una nueva ventana 

![image](https://user-images.githubusercontent.com/119461863/226152020-eaa171da-3515-488f-892e-e2fe85f117b2.png)


![image](https://user-images.githubusercontent.com/119461863/226151316-d3e27213-02dd-473b-807b-e96a751f25c6.png)

# Agregamos el username y password

![image](https://user-images.githubusercontent.com/119461863/226152057-2f486c78-37fd-44fa-bc76-bb64df13c8b7.png)

# Configurando nuestra implementación de Airflow

Para estos pasos es neceserio generar un archivo values.yaml de nuestro gráfico de Helm con el comando:

$ helm show values apache-airflow/airflow > values.yaml

en una nueva terminal de wsl

![image](https://user-images.githubusercontent.com/119461863/226152522-330abf5b-b668-44e5-8767-432a4be1b217.png)

Una vez ejecutado buscamos el archivo "values.yalm" en la parte izquierda de vsc 

![image](https://user-images.githubusercontent.com/119461863/226152605-8704b4a5-248e-4dd9-9e7e-50820b2f9196.png)

Lo abrimos y buscamos las siguientes lineas para modificar "CeleryExecutor" con "LocalExecutor". Reemplace el servicio "ClusterIP" con "LoadBalancer". (Estos servicios se encuentran aproximadamente en las lineas que muestran las imagenes)

![image](https://user-images.githubusercontent.com/119461863/226152288-37b1ad4e-a983-4441-8933-ce512ff05f57.png)
![image](https://user-images.githubusercontent.com/119461863/226152314-881389d1-2c21-4a6a-a3f1-fcae0e3b1a9e.png)

![image](https://user-images.githubusercontent.com/119461863/226152408-0acb0162-2742-4019-855f-7b30f3ac754e.png)
![image](https://user-images.githubusercontent.com/119461863/226152427-b3f73709-b214-4343-a3d8-febf94ea7acf.png)

Guardamos cambios (ctrl + s) y posteriormente ejecutamos el siguiente comando en la terminal de wsl para 
actualizar el cluster

$ helm upgrade --install airflow apache-airflow/airflow -n airflow  \
  -f values.yaml \
  --debug
 
 ![image](https://user-images.githubusercontent.com/119461863/226152927-ef289841-c4e7-4bbc-98da-b54cddfa3af0.png)






Paginas consultadas: https://towardsdatascience.com/deploying-airflow-on-google-kubernetes-engine-with-helm-28c3d9f7a26b 

https://chat.openai.com/chat


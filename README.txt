--------------

Partie Docker

--------------

Installer docker pour ubuntu:

sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

Pour vérifier que tout fonctionne correctement: sudo docker run hello-world

-----------------------------------------------------------------------------
Installer docker-compose :

sudo apt-get update

sudo apt-get install docker-compose-plugin

Pour vérifier que tout fonctionne correctement: docker compose version

-----------------------------------------------------------------------------
Le dossier Docker/Maria-DB contient un Dockerfile et create_structure.sql. Aller dans ce dossier et lancer les commandes suivantes sur créer le docker mariaDB :

Créer l'image mariaDB :    docker build -t cont_mdb .

Lancer le container :   docker run -it -d --name cont_mdb -e MARIADB_USER=user -e MARIADB_PASSWORD=password -e MARIADB_ROOT_PASSWORD=rootpassword cont_mdb

Récuppérer l'adresse IP du container :    docker inspect cont_mdb | grep IPAddress | tail -n 1 

Sauvegarder l'adresse IP du container "cont_mdb"


Le dossier Docker/Python-App contient un Dockerfile. Aller dans ce dossier et lancer les commandes suivantes sur créer le docker python:

Créer l'image mariaDB :    docker build -t cont_python .

Lancer le container, <adresseIP> doit être remplacé par l'adresse IP sauvée précédement :    docker run -ti -e API_USER=root -e API_PASSWORD=rootpassword -e API_IPMDB=<adresseIP> cont_python


------------------
Partie Kubernetes
------------------

Installer minikube: 

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \

  && chmod +x minikube

sudo mkdir -p /usr/local/bin/

sudo install minikube /usr/local/bin/

Pour démarrer minikube :   minikube start

Pour vérifier que tout fonctionne correctement:   minikube status

Doit afficher si tout est installé correctement :

host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

Pour arrêter mikikube :    minikube stop

-----------------------------------------------------------------------------
Installer kubectl: 

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

Pour vérifier que tout fonctionne correctement:    kubectl version --client

-----------------------------------------------------------------------------
Pour utiliser kubernetes :

Aller dans le dossier Kubernetes

pour lancer le fichier :   kubectl apply-f manifest.yaml

vérifier les deploiements ont été lancés :   kubectl get deployments

vérifier les pods ont été lancés :    kubectl get pods

vérifier les log du pod :   kubectl describe <nom-du-pod>

vérifier les services :   kubectl get svc

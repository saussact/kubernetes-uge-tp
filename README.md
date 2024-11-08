# TP Kubernetes (K8S) M2 UGE  2021 - Module DevOps

## Rendu :

Repondre à l'ensemble des questions du TP. Ce TP servira de cours, c'est à vous d'aller chercher les notions. Pour comprendre les thématiques abordés.
Rendre le compte rendu qui vous servira de (cours / fiche de révision) du TP et sera à rendre à la fin.

Vous pouvez créer un branche via master exemple : feature/ <Nom-Prenom>


## 0.  Pré-requis 

Avant de commencer il faut installer : minikube et kubectl (https://kubernetes.io/docs/tasks/tools/install-kubectl/)

## 1.  Quelques notions.
https://www.youtube.com/watch?v=NChhdOZV4sY (fr) ou https://www.youtube.com/watch?v=aSrqRSk43lY (en)

Qu'est ce qu'on pod ? 

Qu'est ce qu'un node ? 

A quoi sert K8S ?

Le développeur s'occupe t'il toujours de l'infrastructure?

Qu'est ce qu'un KUBELET?

Qu'est ce qu'un "Service" dans K8S?

Qu'est ce que EKS? et SWARM?


## 2. Cluster Minikube

Qu'est ce que Minikube?

Lancer `minikube start`

Lancer le dashboard de kubernetes : `minikube dashboard`

Explorer un peu le dashboard pour comprendre l'arborescence.


## 3. Un déploiement K8S
### Deployement

Qu'est ce qu'un déploiement Kubernetes ? 

`kubectl get deployments` 

Qu'avez vous ?

On lance maintenant un déploiement en utilisant l'image docker que nous avions build. (que j'ai déposé sur le dockerhub)

`kubectl create deployment my-app-js --image=tsaussac/node-app`

Relancer  `kubectl get deployments`, le deploiement est lancé ?
 
Aller voir ce qui se passe dans le dashboard.

### Pods
Pour voir l'ensemble des pods qui tournent : `kubectl get pods`

Le pod est t'il "RUNNING" ? S'il ne l'est pas => me le dire.

Pour info : pour détruire un pod utiliser `kubectl delete -n default pod <PODS-ID>`

### Quelques commandes utile :

Voir la config de kubectl : `kubectl config view` 

Voir les events : `kubectl get events`. Avez vous des evenements? si oui, lequel?

`kubectl cluster-info` que donne cette commande? expliquez en deux-trois mots

## 4. Service K8S
Expliquez en quelques mots/lignes ce qu'est un Service dans K8S?

Nous allons créer un service à ce deployment. pour cela on utilise `expose deployment` dans notre cas :

`kubectl expose deployment my-app-js --type=LoadBalancer --port=8080`

Sur Minikube, le type LoadBalancer rend le Service accessible via la commande minikube service

Expliquez ce qu'est un loadbalancer (LB).

Aller voir si vous trouvez le service dans le dashboard et dans le terminal : `kubectl get services`

`minikube service my-app-js`

⚠️ ATTENTION parfois cela peut prendre un peu de temps.

Que se passe'il ? Quel est le message affiché?


## 5. Les extensions

egarder un peu les extensions.
`minikube addons list`

Dans la vie pro vous utiliserez surement : istio, logviewer, metrics-server

Pour ajouter un addon `minikube addons enable metrics-server`

pour l'afficher :

`kubectl get pod,svc -n kube-system`

Expliquer cette commande, pour la comprendre.

## 6. Scaling avec K8S

Lancer 5 exemplaire du pod précédent 

`kubectl scale -n default deployment my-app-js --replicas=5`

A quoi cela sert il (aller chercher sur internet si besoin.)

`kubectl get pods`

Allez voir le dashboard pour comprendre et me dire si c'est cohérent avec le get pods ?

## 7. Creer d’un fichier YAML 

`kubectl get deployment my-app-js -o yaml > my-app-js.yml`

Vous pourrez ainsi directement importer la conf via :  `kubectl create -f <file>`
 
 Expliquer en quelques lignes, quel est l'interet d'avoir ce fichier YAML

## 8. Acceder à un pod  et modifier le message.
 
`kubectl create deployment mynginxapp --image=nginx:latest`

`kubectlexpose deployment mynginxapp --type=NodePort --port=80`

`minikube service mynginxapp --url`

Que voyez vous? Essayez de comprendre les 3 commandes.

Acceder à un pod (nginx) et modifier le fichier index.html.

Récupérer le nom du pods nginx(`kubectl get pods`)

Se connecter à un pod : `kubectl exec -ti mynginxapp-5d9b94449d-lw4jw bash`

`cd /usr/share/nginx/html/`

`ls`

`rm index.html`

`echo "Je ne sais pas quoi ecrire, mais je l'écris...." > index.html`

`exit`

`minikube service mynginxapp --url`

## Cleanning 
Vous pouvez maintenant nettoyer les ressources que vous avez créées dans votre cluster :

`kubectl delete service my-app-js`

`kubectl delete deployment my-app-js`

Si nécessaire, arrêtez la machine virtuelle Minikube (VM) :

`minikube stop`

Si nécessaire, effacez la VM Minikube :

`minikube delete`


## Conclusion

Qu'avez vous pensez du TP ?

Comprennez vous mieux K8S ?

Avez vous des précos ?


## Pour aller plus loin :
- Un ancien collègue d'Orange (Olivier Beyler) à mis en place un cours / Formation K8S très complète...
https://obeyler.github.io/Formation-K8S/

- Aurelie Vache sur Youtube pour comprendre simplement les concepts :
    Understanding Kubernetes in a visual way : https://www.youtube.com/c/AurelieVache/videos


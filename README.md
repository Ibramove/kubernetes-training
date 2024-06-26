Voici un exemple de fichier README pour votre TP3, basé sur les étapes que vous avez décrites :

---

# TP3 Kubernetes Training

Ce dépôt contient les manifestes YAML et les instructions pour déployer une application simple à l'aide de Kubernetes.

## Étapes du TP

### 1. Création du Namespace

Le premier pas consiste à créer un namespace nommé `production` à l'aide d'un manifeste YAML.

```yaml
# namespace.yml

apiVersion: v1
kind: Namespace
metadata:
  name: production
```

Pour déployer ce namespace, utilisez la commande suivante :

```sh
kubectl apply -f namespace.yml
```

### 2. Déploiement du Pod Rouge

Pour déployer un pod avec l'image `mmumshad/simple-webapp-color` affichant la couleur rouge et ayant le label `app: web`, utilisez le manifeste suivant :

```yaml
# pod-red.yml

apiVersion: v1
kind: Pod
metadata:
  name: red-webapp-pod
  namespace: production
  labels:
    app: web
spec:
  containers:
  - name: simple-webapp
    image: mmumshad/simple-webapp-color
    env:
    - name: COLOR
      value: "red"
    ports:
    - containerPort: 8080
```

Pour déployer ce pod, utilisez la commande :

```sh
kubectl apply -f pod-red.yml
```

### 3. Déploiement du Pod Bleu

Pour déployer un pod avec l'image `mmumshad/simple-webapp-color` affichant la couleur bleue et ayant le label `app: web`, utilisez le manifeste suivant :

```yaml
# pod-blue.yml

apiVersion: v1
kind: Pod
metadata:
  name: blue-webapp-pod
  namespace: production
  labels:
    app: web
spec:
  containers:
  - name: simple-webapp
    image: mmumshad/simple-webapp-color
    env:
    - name: COLOR
      value: "blue"
    ports:
    - containerPort: 8080
```

Pour déployer ce pod, utilisez la commande :

```sh
kubectl apply -f pod-blue.yml
```

### 4. Création des Pods

Pour créer les deux pods rouge et bleu dans le namespace `production`, exécutez les commandes précédentes pour `pod-red.yml` et `pod-blue.yml`.

### 5. Service NodePort

Pour exposer les pods via un service de type NodePort sur le port 30008, utilisez le manifeste suivant :

```yaml
# service-nodeport-web.yml

apiVersion: v1
kind: Service
metadata:
  name: web-service
  namespace: production
spec:
  selector:
    app: web
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 8080
    nodePort: 30008
  type: NodePort
```

Pour créer ce service, utilisez la commande :

```sh
kubectl apply -f service-nodeport-web.yml
```

### 6. Vérification du Service

Pour vérifier que le service trouve les deux pods, utilisez la commande suivante :

```sh
kubectl describe service web-service -n production
```

Assurez-vous que la section `Endpoints` liste les adresses IP des pods rouge et bleu.

### 7. Vérification de l'Application

Pour vérifier que l'application est disponible, ouvrez le port 30008 de votre nœud Kubernetes dans votre navigateur ou avec `curl` :

```sh
curl http://<node-ip>:30008
```

Remplacez `<node-ip>` par l'adresse IP de votre nœud Kubernetes.

### 8. Organisation des Manifestes

Créez un répertoire `tp-3` dans `kubernetes-training` et copiez-y tous les manifestes YAML nécessaires.

```sh
mkdir kubernetes-training/tp-3
cp *.yml kubernetes-training/tp-3
```

### 9. Sauvegarde sur GitHub

Poussez ce répertoire sur GitHub pour conserver tous vos fichiers :

```sh
# Assurez-vous d'abord d'initialiser votre repository Git et d'ajouter un remote pour GitHub
git init
git remote add origin <url-du-referentiel-github>
git add .
git commit -m "Ajout des fichiers YAML pour le TP-3"
git push -u origin main
```

---

Ce README vous guide à travers les différentes étapes du TP3 en Kubernetes, en fournissant des instructions claires pour chaque tâche à accomplir. Assurez-vous d'adapter les URLs, les noms de fichiers et les commandes selon votre configuration spécifique.

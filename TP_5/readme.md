
# TP5 - Déploiement de WordPress avec Helm sur Kubernetes

## Objectifs
- Installer Helm
- Déployer WordPress en utilisant un chart Helm
- Configurer un service de type NodePort
- Surcharger les variables de configuration avec un fichier `values.yml`

## Prérequis
- Un cluster Kubernetes opérationnel (Minikube est utilisé dans cet exemple)
- `kubectl` et `helm` installés et configurés

## Étapes

### 1. Démarrer Minikube
Minikube est un outil qui facilite l'exécution de Kubernetes localement. Assurez-vous que Minikube est installé et démarrez-le :

```sh
minikube start
```

### 2. Configurer le contexte Kubernetes
Vérifiez que `kubectl` est configuré pour utiliser le contexte Minikube :

```sh
kubectl config use-context minikube
```

### 3. Vérifier la connexion au cluster
Assurez-vous que `kubectl` peut se connecter à votre cluster Kubernetes :

```sh
kubectl cluster-info
```

Vous devriez voir des informations sur votre cluster si tout fonctionne correctement.

### 4. Installer Helm
Helm est un gestionnaire de paquets pour Kubernetes. Installez Helm en utilisant la commande suivante :

```sh
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

Vérifiez que Helm est correctement installé :

```sh
helm version
```

### 5. Ajouter le dépôt de charts Helm Bitnami
Ajoutez le dépôt de charts Bitnami à Helm :

```sh
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

### 6. Créer le fichier `values.yml`
Créez un fichier nommé `values.yml` pour surcharger les valeurs par défaut du chart WordPress. Ce fichier contiendra les paramètres spécifiques que nous voulons modifier, notamment le service de type NodePort et les informations de connexion à WordPress.

Contenu du fichier `values.yml` :

```yaml
wordpressUsername: admin
wordpressPassword: password
service:
  type: NodePort
  nodePorts:
    http: 30080  # Choisissez le port que vous souhaitez
```

### 7. Déployer WordPress avec Helm
Utilisez Helm pour déployer WordPress en utilisant le fichier `values.yml` que vous avez créé :

```sh
helm install my-wordpress bitnami/wordpress -f values.yml
```

### 8. Vérifier le déploiement
Une fois le déploiement terminé, vérifiez que les pods sont en cours d'exécution :

```sh
kubectl get pods
```

Pour obtenir l'URL du service WordPress, utilisez la commande suivante :

```sh
minikube service my-wordpress --url
```

### 9. Organisation des fichiers et push sur GitHub
Créez un répertoire `tp-5` dans votre dépôt `Kubernetes-training` et placez-y les fichiers nécessaires.

#### Étapes détaillées :

1. **Cloner le dépôt Kubernetes-training** :

    ```sh
    git clone https://github.com/votre-utilisateur/Kubernetes-training.git
    cd Kubernetes-training
    mkdir tp-5
    ```

2. **Créer le fichier `values.yml`** :

    ```sh
    cd tp-5
    nano values.yml
    # Copier le contenu ci-dessus dans le fichier values.yml
    ```

3. **Ajouter les fichiers au dépôt et les pousser sur GitHub** :

    ```sh
    cd ..
    git add tp-5
    git commit -m "Ajout des fichiers pour le déploiement de WordPress avec Helm"
    git push origin main
    ```

### Conclusion
En suivant ces étapes, vous aurez installé Helm, déployé WordPress en utilisant un chart Helm avec un service de type NodePort, et sauvegardé vos configurations dans un dépôt GitHub.

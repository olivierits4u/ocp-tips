# ocp-tips

## build config avec git password & config map

cas d'utilisation: un build config qui utilise un repo git privé, et qui a besoin d'un fichier "settings.xml" custom pour les dépendences maven

```
#création du secret
oc create secret generic githubsecret \
	 --type kubernetes.io/basic-auth \
	 --from-literal password=MY_PASSWORD \
	 --from-literal username=MY_USERNAME

#création du build config
oc new-app  \
	 --name api    \
	 --source-secret=githubsecret  \
	 --as-deployment-config  \
	 java:openjdk-11-ubi8~https://github.com/XXXX/YYYY

#création de la config map
oc create cm build-cm --from-file=settings.xml



```
ensuite éditer le build config
```
  source:
    git:
      uri: https://github.com/XXXX/YYYY
    sourceSecret:
      name: github
    configMaps:
      - configMap:
          name: build-cm
        destinationDir: /tmp/src/configuration
```

# ocp-tips

## build config & git password & config map pour le build config

```
#création du secret
oc create secret generic githubsecret \
	 --type kubernetes.io/basic-auth \
	 --from-literal password=MY_PASSWORD \
	 --from-literal username=MY_USERNAME

#création de la config map
oc create cm build-cm --from-file=settings.xml



```
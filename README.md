# ocp-tips

##build config & git password & config map pour le build config

```
#création du secret
oc create secret generic githubsecret \
	 --type kubernetes.io/basic-auth --from-literal password=MY_PASSWORD --from-literal username=MY_USERNAME

```
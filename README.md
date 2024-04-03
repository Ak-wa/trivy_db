# trivy_db
Trivy database for use in airgaped environment

Since dbv1 is deprecated, trivy-db as exported db file has to be built manually
https://aquasecurity.github.io/trivy/v0.41/docs/advanced/air-gap/   

To get all yaml files from k8s, use 
```
for i in $(kubectl get pods --all-namespaces --template '{{range .items}}{{.metadata.namespace}}|{{.metadata.name}}{{"\n"}}{{end}}'); do
	
	ns=$(echo $i| awk -F '|' '{print $1}'); 
	pod=$(echo $i| awk -F '|' '{print $2}');

	echo "[+] namespace: $ns ";
	echo "    pod:       $pod";
	echo "    dump pod yaml description"
	kubectl -n $ns get pods ${pod} -o yaml > ns-${ns}_${pod}.yaml
	
done
```

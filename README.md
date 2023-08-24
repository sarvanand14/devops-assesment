# devops-assesment

1.Deploy postgres as statefulset in kubernetes
  
 deployed a postgres statefulset from helm using the below commmand
  
    -  helm install my-release oci://registry-1.docker.io/bitnamicharts/postgresql


2. Deploy prometheus in the cluster

     added the helm repo for the prommetheus.

       helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
       helm repo update

   Install the prometheus chart

       helm install prometheus-test prometheus-community/prometheus

3.  Postgres exporter

    deployed the postgres exporter using helm with the following commands

        helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
        helm repo update


    Install the postgres-exporter chart

        helm install exporter prometheus-community/prometheus-postgres-exporter



fetched  the exporter svc name using the below command 
     
     kubectl get svc 
add the exporter service name in the prometheus targets section  in  values.yaml file
     
     - targets:
        - exporter-prometheus-postgres-exporter

After adding the exporter details upgrade the prometheus helm chart with the following command

      helm upgrade prometheus-test  prometheus-community/prometheus -f values.yaml

We can now find  the postgres-exporter in the targets  section and we can also see the exporter in query when we check for "pg_exporter_scrapes_total" 

![image](https://github.com/sarvanand14/devops-assesment/assets/142403605/f349d631-0518-41b9-91a5-53ecc3509696)



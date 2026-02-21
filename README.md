EKS Cluster

             ── Proxy Deployment (2 replicas)

             ── Proxy Service (LoadBalancer)

             ── Backend Deployment (3 replicas)

             ── Backend Service (ClusterIP) 

 reverse-proxy-project/

        ── reverse-proxy-deployment.yaml

        ── reverse-proxy-service.yaml

         ── backend-deployment.yaml

          ── backend-service.yaml

         ── nginx.conf   (your reverse proxy config)

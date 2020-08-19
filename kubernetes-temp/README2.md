An example Ingress that makes use of the controller:

  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls



nginx-ingress-controller   LoadBalancer   10.27.255.49   35.185.232.144   80:32566/TCP,443:32124/TCP   3m52s   app.kubernetes.io/component=controller,app=nginx-ingress,release=nginx-ingress

35.185.232.144




nginx-ingress   pod/nginx-ingress-controller-5ddbdf4fc9-cj7fv                     1/1     Running   0          5m18s
nginx-ingress   pod/nginx-ingress-default-backend-5b967cf596-z59lx                1/1     Running   0          5m18s


nginx-ingress   service/nginx-ingress-controller        LoadBalancer   10.27.255.49    35.185.232.144   80:32566/TCP,443:32124/TCP   5m20s
nginx-ingress   service/nginx-ingress-default-backend   ClusterIP      10.27.253.230   <none>           80/TCP                       5m20s



nginx-ingress   deployment.apps/nginx-ingress-controller                   1/1     1            1           5m20s
nginx-ingress   deployment.apps/nginx-ingress-default-backend              1/1     1            1           5m20s




nginx-ingress   replicaset.apps/nginx-ingress-controller-5ddbdf4fc9                   1         1         1       5m20s
nginx-ingress   replicaset.apps/nginx-ingress-default-backend-5b967cf596              1         1         1       5m20s






kubectl get service nginx-ingress-controller -n nginx-ingress -o yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
    meta.helm.sh/release-name: nginx-ingress
    meta.helm.sh/release-namespace: nginx-ingress
  creationTimestamp: "2020-08-12T11:12:35Z"
  finalizers:
  - service.kubernetes.io/load-balancer-cleanup
  labels:
    app: nginx-ingress
    app.kubernetes.io/managed-by: Helm
    chart: nginx-ingress-1.41.2
    component: controller
    heritage: Helm
    release: nginx-ingress
  name: nginx-ingress-controller
  namespace: nginx-ingress
  resourceVersion: "101411"
  selfLink: /api/v1/namespaces/nginx-ingress/services/nginx-ingress-controller
  uid: 6b66f54f-b658-48a5-b585-ab8ee11e60f5
spec:
  clusterIP: 10.27.255.49
  externalTrafficPolicy: Cluster
  ports:
  - name: http
    nodePort: 32566
    port: 80
    protocol: TCP
    targetPort: http
  - name: https
    nodePort: 32124
    port: 443
    protocol: TCP
    targetPort: https
  selector:
    app: nginx-ingress
    app.kubernetes.io/component: controller
    release: nginx-ingress
  sessionAffinity: None
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - ip: 35.185.232.144











kubectl get service nginx-ingress-default-backend -n nginx-ingress -o yaml

apiVersion: v1
kind: Service
metadata:
  annotations:
    meta.helm.sh/release-name: nginx-ingress
    meta.helm.sh/release-namespace: nginx-ingress
  creationTimestamp: "2020-08-12T11:12:35Z"
  labels:
    app: nginx-ingress
    app.kubernetes.io/managed-by: Helm
    chart: nginx-ingress-1.41.2
    component: default-backend
    heritage: Helm
    release: nginx-ingress
  name: nginx-ingress-default-backend
  namespace: nginx-ingress
  resourceVersion: "101183"
  selfLink: /api/v1/namespaces/nginx-ingress/services/nginx-ingress-default-backend
  uid: cdc82f6c-c267-4195-8eab-e5836ce19147
spec:
  clusterIP: 10.27.253.230
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: http
  selector:
    app: nginx-ingress
    app.kubernetes.io/component: default-backend
    release: nginx-ingress
  sessionAffinity: None
  type: ClusterIP
status:
  loadBalancer: {}





Установка - 
nginx
cert
    создать issuers


kubectl create ns hipster-shop




 helm secrets upgrade --install frontend  kubernetes-temp/frontend/ --namespace hipster-shop \
      -f  kubernetes-temp/frontend/values.yaml \
      -f  kubernetes-temp/frontend/secrets.yaml


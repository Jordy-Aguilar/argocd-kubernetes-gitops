Automatizacion GitOps con Argo CD y Kubernetes

Repositorio fuente: https://github.com/Jordy-Aguilar/argocd-kubernetes-gitops

Archivos para publicar:
- k8s/deployment.yml: Nginx, 2 replicas iniciales, labels, probes, requests y limits.
- k8s/service.yml: NodePort 30080 para acceder a la aplicacion.
- k8s/hpa.yml: CPU al 50%, entre 2 y 5 replicas.
- bootstrap/application.yml: aplicacion Argo CD, auto-sync y exclusion de spec.replicas
  para que el HPA administre la cantidad de Pods sin ser revertido por GitOps.

El Application apunta a la carpeta k8s. Por eso bootstrap/application.yml queda
fuera de esa ruta y Argo CD no intenta gestionarse recursivamente a si mismo.

La interfaz accesible por NodePort mostrara la pagina por defecto de Nginx.
Metrics Server debe estar instalado y Ready antes de probar el HPA.
El escalado puede tardar en reflejarse; el objetivo de 50% se mide con relacion
a requests.cpu. No se deben incluir claves, tokens ni kubeconfig en GitHub.

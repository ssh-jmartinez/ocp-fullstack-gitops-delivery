# Enterprise GitOps & CI/CD Orchestration on OpenShift

Este repositorio centraliza la orquestación, automatización y los manifiestos de infraestructura para una aplicación Full-Stack distribuida. El objetivo principal es demostrar un flujo de entrega continua (CI/CD) profesional utilizando herramientas nativas de Kubernetes en un entorno de **Red Hat OpenShift**.

---

## 🏗️ Arquitectura del Sistema

La solución se basa en una arquitectura de microservicios desacoplada, donde la seguridad y la conectividad se gestionan a nivel de infraestructura:

![Arquitectura Técnica del Proyecto](./assets/arquitectura.png)

### Ecosistema de Aplicaciones
El código fuente de los componentes se mantiene en repositorios independientes para facilitar el escalado y la mantenibilidad:

* **Frontend Service:** [demo-app](https://github.com/jmartinez-fusion/demo-app.git) - Host estático basado en Nginx Unprivileged que integra las reglas de Reverse Proxy.
* **Backend Service:** [demo-backend](https://github.com/jmartinez-fusion/demo-backend.git) - API REST en Node.js encargada del procesamiento de datos.
* **Database:** Instancia persistente de PostgreSQL gestionada mediante **Persistent Volume Claims (PVC)**.

---

## ⚙️ Estrategia de Diseño y Decisiones Técnicas

En lugar de un despliegue tradicional, se optó por un enfoque de **Infraestructura como Código (IaC)** basado en los siguientes principios:

### 1. Centralización de la Conectividad (Reverse Proxy)
Se decidió utilizar Nginx no solo como servidor de archivos, sino como un **Punto de Entrada Unificado**. 
* **Por qué:** Al redirigir el tráfico `/api` internamente hacia el backend, eliminamos la necesidad de configurar políticas de CORS en el código y simplificamos el DNS, exponiendo un único punto de entrada (Route) hacia el exterior.

### 2. Entrega Basada en GitOps (Argo CD)
Toda la configuración del clúster reside en este repositorio de manifiestos utilizando el patrón **App-of-Apps**.
* **Por qué:** Esto garantiza que el estado del clúster sea auditable y recuperable. Si un objeto de Kubernetes se modifica manualmente, Argo CD detecta la desviación ("drift") y lo sincroniza automáticamente con la versión definida en Git.

### 3. Pipelines de Construcción Nativos (Tekton)
El proceso de CI se ejecuta dentro del propio clúster mediante **Tekton Pipelines**.
* **Por qué:** Al usar Buildah para la construcción de imágenes, el proceso es más seguro (daemonless) y se integra perfectamente con el registro de imágenes interno de OpenShift, reduciendo la latencia y mejorando la seguridad del ciclo de vida de la imagen.

### 4. Gestión Segura de Secretos (Sealed Secrets)
Se implementó **Bitnami Sealed Secrets** para gestionar credenciales de base de datos.
* **Por qué:** Permite cifrar secretos de forma que solo el controlador dentro del clúster pueda descifrarlos. Esto hace posible almacenar información sensible de forma segura en este repositorio público, manteniendo el flujo 100% fiel a la filosofía GitOps.

---

## 🚀 Estructura del Repositorio de Orquestación

Este repositorio está organizado para separar la lógica de automatización de los recursos de Kubernetes:

* **`/k8s-manifests`**: Contiene los Deployments, Services, Routes y definiciones de **SealedSecrets** (provisionamiento automático de credenciales cifradas).
* **`/argocd-apps`**: Definiciones de las aplicaciones de Argo CD (Root App y Templates) para la gestión del ciclo de vida jerárquico.
* **`/pipeline`**: Definiciones de Tasks y Pipelines de Tekton para el flujo de CI.
* **`/cicd`**: Configuraciones críticas de entorno, incluyendo el Dockerfile optimizado para entornos unprivileged y la configuración del proxy de red.

---

## 💻 Tecnologías Core
* **Orquestación:** Red Hat OpenShift
* **GitOps:** Argo CD
* **CI Pipelines:** Tekton
* **Container Build:** Buildah
* **Seguridad:** Bitnami Sealed Secrets
* **Stack:** Nginx, Node.js, PostgreSQL
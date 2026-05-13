# ENTERPRISE GITOPS PLATFORM ON RED HAT OPENSHIFT

<p align="center">
  Plataforma GitOps enterprise end-to-end enfocada en automatización, seguridad Zero Trust, observabilidad y progressive delivery sobre Red Hat OpenShift.
</p>

---

## Arquitectura General

<p align="center">
  <img src="./docs/architecture/platform-overview.png" alt="Enterprise GitOps Platform" width="100%">
</p>

---

# Visión General

Este repositorio representa una plataforma GitOps enterprise completa construida sobre Red Hat OpenShift.

El objetivo principal del proyecto es demostrar cómo diseñar una infraestructura moderna basada en:

- GitOps
- CI/CD declarativo
- Seguridad Zero Trust
- Progressive Delivery
- Gestión segura de secretos
- Observabilidad en tiempo real
- Automatización end-to-end

Todo gestionado como código.

---

# Stack Tecnológico

## Plataforma

- Red Hat OpenShift
- Kubernetes
- OpenShift Pipelines (Tekton)

## GitOps

- Argo CD
- Argo Rollouts

## Seguridad

- Network Policies
- RBAC
- Pod Security
- Bitnami Sealed Secrets

## Observabilidad

- Prometheus
- Grafana

## Aplicación Demo

- Frontend: Nginx
- Backend: Node.js
- Database: PostgreSQL

---

# Objetivo del Repositorio

Este proyecto NO busca mostrar solamente una aplicación.

Busca representar cómo podría verse una plataforma enterprise real en producción utilizando prácticas modernas de:

- Infraestructura como Código
- GitOps
- Entregas progresivas
- Seguridad por diseño
- Automatización declarativa
- Observabilidad integrada

---

# Estructura del Proyecto

La estructura está organizada para separar claramente cada dominio de la plataforma.

```bash
.
├── argocd-apps/
├── k8s-manifest/
├── observability/
├── docs/
├── scripts/
└── README.md
```

---

# Directorio Principal: `k8s-manifest`

Dentro de `k8s-manifest` se encuentran las distintas capas de la plataforma.

Cada directorio representa una etapa funcional del entorno enterprise.

```bash
k8s-manifest/
├── 01-core/
├── 02-security/
└── 03-advanced-delivery/
```

---

# ¿Qué contiene cada directorio?

## `01-core`

Infraestructura base de Kubernetes/OpenShift.

Ejemplos:

- Namespaces
- ConfigMaps
- Services
- Ingress
- Storage
- Recursos base de aplicaciones

También puede incluir la evolución inicial del entorno por proyecto o por día.

---

## `02-security`

Capa de seguridad Zero Trust.

Ejemplos:

- Network Policies
- RBAC
- Pod Security
- Sealed Secrets
- Restricciones de tráfico
- Seguridad declarativa

Aquí se documenta cómo fue evolucionando la seguridad del cluster y las aplicaciones.

---

## `03-advanced-delivery`

Entrega progresiva y automatización avanzada.

Ejemplos:

- Argo Rollouts
- Canary Deployments
- Blue/Green
- Traffic Shifting
- Auto Rollback
- Progressive Delivery

Este directorio contiene las implementaciones avanzadas relacionadas al ciclo de entrega de aplicaciones.

---

# Organización Interna

Cada subdirectorio puede contener:

- manifests YAML
- overlays
- pruebas
- ejemplos
- snapshots
- implementaciones por proyecto
- implementaciones por día
- documentación técnica específica

La idea es que el repositorio funcione tanto como:

- laboratorio práctico,
- referencia técnica,
- documentación viva,
- plataforma reusable.

---

# GitOps Bootstrap

Todo el proyecto puede desplegarse utilizando Argo CD.

Una vez instalado Argo CD en OpenShift, ejecutar:

```bash
argocd app create -f argocd-apps/root-app.yaml
```

Esto desplegará automáticamente toda la estructura declarativa definida en el repositorio.

---

# ¿Qué hace el Root Application?

El `root-app.yaml` actúa como punto central de sincronización GitOps.

Desde allí:

- Argo CD sincroniza todas las aplicaciones
- se despliegan los manifests automáticamente
- se mantienen los estados declarativos
- se aplica la estructura completa de la plataforma

Esto permite administrar toda la infraestructura desde Git.

---

# Flujo General de la Plataforma

```text
GitHub
   ↓
Tekton Pipelines
   ↓
Container Registry
   ↓
Argo CD
   ↓
OpenShift Cluster
   ↓
Argo Rollouts
   ↓
Canary / Progressive Delivery
   ↓
Observabilidad + Seguridad
```

---

# Características Principales

## GitOps Declarativo

Toda la plataforma es gestionada desde Git.

---

## Seguridad Zero Trust

El tráfico entre workloads está controlado mediante Network Policies.

---

## Progressive Delivery

Implementaciones Canary utilizando Argo Rollouts.

---

## Gestión Segura de Secretos

Uso de Bitnami Sealed Secrets para proteger credenciales sensibles.

---

## Observabilidad Integrada

Métricas y monitoreo utilizando Prometheus y Grafana.

---

## Infraestructura Reproducible

Toda la plataforma puede recrearse automáticamente desde manifests declarativos.

---

# Requisitos

- OpenShift Cluster
- Argo CD
- OpenShift Pipelines
- Acceso administrativo al cluster
- CLI:
  - oc
  - kubectl
  - argocd

---

# Filosofía del Proyecto

Este repositorio fue diseñado con una idea clara:

> tratar infraestructura, seguridad y delivery como un ecosistema integrado y observable.

No como componentes aislados.

---

# Autor

```text
Javier Martínez | DevOps
```

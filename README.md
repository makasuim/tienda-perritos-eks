# Tienda de Perritos - Pipeline CI/CD en AWS EKS 🐾

Este es nuestro repositorio para el encargo de **Innovatech Chile**. Aquí está todo el código y la configuración que armamos para que la aplicación (Frontend, Backend y Base de Datos) se despliegue de forma automatizada y escalable en la nube.

## Tecnologías y Arquitectura
* **Orquestación:** Amazon EKS.
* **Contenedores:** Docker y Amazon ECR (para almacenar las imágenes).
* **CI/CD:** GitHub Actions.
* **Redes:** Balanceador de carga (ALB), VPC y subredes.
* **Autoscaling:** HPA (Horizontal Pod Autoscaler) configurado para escalar si el backend supera el 50% de uso de CPU.

## Estructura del Repositorio
* `/frontend`: Código fuente y Dockerfile del cliente web.
* `/backend`: Código fuente y Dockerfile de la API.
* `/db`: Configuración de la base de datos.
* `/k8s`: Todos los manifiestos de Kubernetes (Deployments, Services, HPA).
* `.github/workflows`: Contiene el archivo `deploy-eks.yml` que ejecuta el pipeline.

## ¿Cómo funciona el despliegue?

Todo el proceso está automatizado. Cada vez que hacemos un `push` a la rama `main`, GitHub Actions se encarga de:
1. Armar las nuevas imágenes de Docker.
2. Subirlas a nuestros repositorios privados en Amazon ECR.
3. Actualizar los pods directamente en el clúster de EKS.

**Para aplicar cambios manuales en el clúster:**
Asegúrate de tener tus credenciales de AWS configuradas y ejecuta:
```bash
kubectl create namespace tienda
kubectl apply -f k8s/

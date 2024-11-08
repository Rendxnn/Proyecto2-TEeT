# Proyecto 2: Tópicos de Telemática ST0263

## Estudiantes
- **Jaime Uribe**: jruribem@eafit.edu.com
- **Juan Pablo Duque**: jpduquep@eafit.edu.co
- **Samuel Rendon**: jpduquep@eafit.edu.co

## Profesor
- **Alvaro Enrique Ospina Sanjuan**: aeospinas@eafit.edu.co

## 1. Descripcion
El reto consistió en el despliegue de un cluster de Kubernetes de alta disponibilidad para una página un CMS Wordpress (Inicialmente se intentó Moodle y Drupal pero se encontraron inconvenientes, finalmente funcionó con wordpress) en un cluster de microk8s en nube (GCP), con almacenamiento persistente (Instancia nfs), base de datos (MYSQL), balanceador de carga (NGINX), con certificado SSL para conexión a través de https.

## 1.1. Que aspectos cumplió o desarrolló de la actividad propuesta por el profesor (requerimientos funcionales y no funcionales)

Se cumplió con todos los requisitos de la actividad.
[Ver pantallazos más abajo]


# 2. información general de diseño de alto nivel, arquitectura, patrones, mejores prácticas utilizadas.

La arquitectura se basa en la replicación de pods con imágenes de componentes de software que entre sí aseguran la alta disponbilidad constante en la aplicación.

Se crea dentro del cluster servicios de Mysql, Wordpress y Nginx para la base de datos, muestra de informacion y balanceo de carga respectivamente. Por fuera del cluster se encuentra la instancia nfs con el almacenamiento persistente tanto de la base de datos como del contenido de la página.

# 3. Descripción del ambiente de desarrollo y técnico: lenguaje de programación, librerias, paquetes, etc, con sus numeros de versiones.

Lenguaje de programación: YAML.
Todo el despliegue se realiza por medio de archivos YAML para la definición de despliegue de servicios, creación de pods, creación de PV's (Persistent Volumes) y PVC's (Persistent Volume Claims) para la interacción con el NFS, y demás.

Todos los códigos y comandos utilizados para el despliegue se pueden encontrar en la carpeta correspondiente a cada servicio en el presente repositorio.

# 4. Descripción del ambiente de EJECUCIÓN (en producción) lenguaje de programación, librerias, paquetes, etc, con sus numeros de versiones.

Instancias creadas:

![image](https://github.com/user-attachments/assets/13e1de33-fa01-4a9e-a6d3-c5c97e030c2e)
Se usaorn replicas de una imagen de instancia e2medium con microk8s instalado.

Cluster creado:
![image](https://github.com/user-attachments/assets/bb3220e5-b80c-4678-835d-10e34f76705b)


Servicios corriendo:
![image](https://github.com/user-attachments/assets/c734ea51-082e-4029-b690-1ab4b09925ef)


Pods corriendo:
![image](https://github.com/user-attachments/assets/fd28cb79-020f-4aa1-ba46-09f002511bea)


Página montada:
![image](https://github.com/user-attachments/assets/50eb1eea-9614-4d0d-8423-ddef3f0bed89)


Conexión segura (https, ssl):
![image](https://github.com/user-attachments/assets/aa0a9409-f7fc-4fee-acc7-b32c4a9866c9)


Configuracion DNS (GoDaddy):
![image](https://github.com/user-attachments/assets/1bcfce79-57e2-4da8-b18e-1c1f94e4c2c7)


# 5. otra información que considere relevante para esta actividad.

### COMANDOS MÁS UTILIZADOS:

Aplicar cambios en un servicio y crear pods: 
```{bash}

kubectl apply -f <nombredelarchivo.yaml>

```

Ver información relevante sobre un pod o servicio
```{bash}

kbuectl describe <pod-servicio-segunelcaso> <nombredepodoservicio>

```

Entrar a un pod
```{bash}

kubectl exec -it <nombredelpod> -- /bin/bash

```


Problemas encontrados:

El principal problema que se encontró durante el desarrollo de la actividad fue la configuración del Ingress para el acceso a la página, que finalmente se solucionó creando el ingress directamente por el dominio. Perdimos bastante tiempo intentando ingresar con la ip de algun nodo. también se tuvo problemas con la carga de archivos de configuración compartidos de Wordpress al NFS, resultando en dificultades para subir imágenes a la página desplegada.







# Pasos realizados para el despliegue de la Aplicación Pokedex

El acontinuacion se detalla la bitácora técnica detallada del despliegue del código fuente de Pokedex hacia la infraestructura de Microsoft Azure. Se documentaron los comandos de terminal ejecutados, las configuraciones de la plataforma de nube y las adaptaciones especiales aplicadas al código para garantizar la visualización correcta y el cumplimiento de las normativas de seguridad (Calificación A+).
## Paso: 1nicialización del Repositorio Local y Remoto
Como primer requisito, se preparó el control de versiones conectando el código local con un repositorio en la nube.
1. se creo del repositorio, se accedió a GitHub y se creó un repositorio público totalmente vacío nombrado exactamente "pokedex".
2. Inicialización de Git: Desde la terminal de Visual Studio Code, ubicados en la carpeta raíz del proyecto, se ejecutaron los siguientes comandos para subir el código fuente inicial:
   bash
 "git init"
Inicializador del repositorio local de Git
"git add"
 se agregaron todos los archivos del proyecto al área de preparación (staging).
"git commit -m "inicio del repositorio base de Pokedex"
   se Crea el primer commit con los archivos
"git remote add origin [https://github.com/ehcarey/pokedex]
 se vincula el repositorio local con el repositorio remoto de GitHub
   git remote add origin [https://github.com/ehcarey/pokedex]
se sube el código a la nube estableciendo la rama 'main' como origen por defecto
   git push -u origin main

## Paso 2: Configuración del Recurso en Azure Static Web Apps
 Con el código en GitHub, se procedió a configurar el servidor en la nube de Azure.
1. Creación del Recurso: En el Portal de Azure, se buscó el servicio "Static Web Apps" y se seleccionó "Crear".
Datos Básicos:
Suscripción: Azure for Students.
Grupo de recursos: Se creó uno nuevo llamado rg-pokedex
Nombre de la aplicación estática: app-pokedex.
Tipo de plan de hospedaje: Gratuito (Free).
Región: Se seleccionó la región más cercana disponible (ej. East US 2).
2. Detalles de Implementación:
Origen: GitHub. Se autorizó la conexión entre Azure y GitHub.
Organización: Cuenta personal.
Repositorio: pokedex.
Rama: main.
Detalles de Compilación (Configuración Crítica):
Valores preestablecidos de compilación: Angular.
Ubicación de la aplicación (App location): /source/pokedex "https://github.com/ehcarey/pokedex/blob/main/source/pokedex/package.json".
Ubicación de salida (Output location): dist/pokedex.
Se hizo clic en "Revisar y crear" y luego en "Crear". Azure configuró automáticamente un flujo de trabajo (Workflow) en GitHub Actions para compilar y desplegar la app.

## Paso 3: Configuración Especial (Corrección de Rutas de Activos)

Tras el primer despliegue automático, se evidenció que las imágenes de los Pokémon no se renderizaban. Esto se debía a que el código original estaba configurado con una ruta base diseñada para GitHub Pages (/pokedex-angular/assets/...), mientras que Azure Static Web Apps despliega los recursos estáticos directamente en la raíz absoluta.
1. Intervención técnica:
Se modificó el archivo de configuración para entornos de producción ubicado en src/environments/environment.prod.ts.
Estado original (Línea 9):imagesPath: '/pokedex-angular/assets/images',
Configuración corregida (Línea 9):imagesPath: '/assets/images',
Se integró este cambio al repositorio ejecutando:
git add .
git commit -m "fix: ajuste de rutas absolutas para renderizado de imagenes en Azure"
git push
 
## Paso 4: Implementación de Encabezados de Seguridad (Meta: Calificación A+)
 Para cumplir con el estándar de ciberseguridad exigido y asegurar la máxima nota en el escáner de securityheaders.com, se implementaron las políticas CSP, HSTS, y protección contra Clickjacking (X-Frame-Options).

Procedimiento:
1. Se creó un archivo nativo de configuración de Azure llamado staticwebapp.config.json exactamente dentro del directorio source/pokedex/ (el mismo nivel del app_location).
2. Se inyectó la siguiente estructura JSON que Azure lee automáticamente durante el despliegue para sobrescribir las cabeceras HTTP del servidor:
{
  "globalHeaders": {
    "Content-Security-Policy": "default-src 'self' https: 'unsafe-inline' 'unsafe-eval'",
    "Strict-Transport-Security": "max-age=31536000; includeSubDomains",
    "X-Frame-Options": "SAMEORIGIN",
    "X-Content-Type-Options": "nosniff",
    "Referrer-Policy": "strict-origin-when-cross-origin"
  }
}
3. Se aplicaron los cambios en el servidor mediante Git:
git add .
git commit -m "Encabezados de seguridad"
git push

cuando se finalizo el flujo de trabajo de GitHub Actions, la aplicación se hizo accesible públicamente. Al someter la URL definitiva al escáner de seguridad, se confirmó la correcta inyección de las cabeceras a través del archivo de configuración sin alterar el código de Angular, obteniendo exitosamente la calificación A+.

> Written with [StackEdit](https://stackedit.io/).
# Creación de Cuenta en Azure for Students

Este documento detalla el paso a paso para la creación de la cuenta en la nube pública utilizada para el despliegue del proyecto Pokedex.

## Paso 1: Acceso al portal
se ingreso a la página oficial de **Azure for Students** hacer  clic en el botón "Start free" (Comenzar gratis).

## Paso 2: Autenticación con el correo institucional
se inicia sesión utilizando el correo electrónico institucional del Tecnológico Comfenalco. Se uso esta cuanta académica para que Microsoft validara automáticamente el estado de estudiante sin necesidad de registrar una tarjeta de crédito.

## Paso 3: Verificación de identidad
1. Tras iniciar sesión, Azure requiere una verificación de identidad adicional.
2. Se proporcionó un número de teléfono móvil válido o autenticación atreves de la app authenticator.
3. Se ingresa el código de verificación recibido para confirmar la cuenta.
4. Se completó el formulario de perfil con el nombre completo y datos de contacto básicos.


## Paso 4: Activación y Configuración Inicial de la Suscripción
1. Se leyeron y aceptaron los términos del acuerdo de suscripción de Microsoft.
2. Al hacer clic en "Registrarse", el sistema aprovisionó automáticamente una suscripción de "Azure for Students".
3. Una vez dentro del Portal de Azure** (`portal.azure.com`), se verificó en el menú lateral izquierdo, haciendo clic en **"Suscripciones"** (Subscriptions). Confirmando que aparezca una suscripción denominada "Azure for Students" y que su estado actual indique "Activa".

## Paso 5: Preparación del Entorno:
1. Con la suscripción activa, la cuenta tiene USD $100 en créditos académicos y acceso a servicios gratuitos por 12 meses, dejando el entorno de nube completamente configurado y listo para iniciar la creación del recurso.
2. Creación del Recurso Static Web Apps En la barra de búsqueda superior del portal, escribir y seleccionar "Static Web Apps" (Aplicaciones web estáticas).
3. Se hace clic en el botón "Crear" para iniciar el asistente de configuración del servicio.

## Paso 6: Configuración de los Detalles Básicos:
1. Suscripción: Se selecciona Azure for Students para aplicar los créditos académicos y evitar cargos monetarios.
2. Grupo de recursos: se crea un grupo (por ejemplo, rg-pokedex-app) para mantener organizado el proyecto en la nube.
3. Nombre de la aplicación estática: Se le asigna un nombre único al recurso.
4. Se elije el tipo de plan se debe elegir la opción Gratis (Free).
5. Seleccionar la zona geográfica más cercana y óptima (por ejemplo, East US 2).


> Written with [StackEdit](https://stackedit.io/).
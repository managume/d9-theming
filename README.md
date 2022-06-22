# Drupal 9 Theming

** Creando un tema custom para Drupal 9 con Drush **

Seguir los siguientes pasos para levantar el proyecto de prueba:

* Lanzar `git clone git@github.com:managume/d9-theming.git` para descargar el proyecto y `ddev start`para levantarlo con DDEV:

* Para abrir el proyecto en el navegador, bien utilizamos el comando `ddev launch` o abrimos las url `d9-theming.ddev.site` en el navegador.

* Para abrir el código en Visual Studio Code, nos situamos en la raíz del proyecto y lo abrimos con `code .`.

## Instrucciones para crear un tema custom con Drupal 9 y Drush

* Vamos a crear un nuevo tema partiendo de la herramienta Drush y del tema `starterkit_theme` que habita en el core de Drupal (`web/core/themes/starterkit_theme`).

* Para comprobar que tenemos Drush en nuestro proyecto funcionando correctamente, lanzamos `ddev drush`.

* Con esto, solamente nos falta lanzar un comando que nos cree nuestro nuevo tema custom a partir de uno ya existente, que lo tomaremos de base. Esto se hace lanzando el comando `ddev drush gen theme`. Este comando lanzará un asistente que nos hará las siguientes preguntas:

  * Título del tema --> `Drupal 9 Theming`
  * Nombre máquina del tema --> `d9_theming`
  * Tema base --> `starterkit_theme`
  * Descripción --> `My new custom theme in Drupal 9`
  * Package --> `Custom`
  * Uso de SASS --> `No`
  * Crear breakpoints --> `No`
  * Crear formulario de configuración del tema --> `No`

Y voilà, tenemos nuestro nuevo tema custom disponible en `web/themes/d9_theming`

* Para activar nuestro nuevo tema, bien por interfaz a través de la sección *Apariencia*, o haciendo uso de Drush lanzando el comando `ddev drush then d9_theming`.

* Siempre que hagamos algún cambio en la configuración de Drupal, es aconsejable lanzar `ddev drush cr` para hacer una limpieza de caché.

## Estructura de nuestro tema custom

* d9_theming
  * css
  * images
  * js
  * templates
  * d9_theming.info.yml
  * d9_theming.libraries.yml
  * d9_theming.theme
  * logo.svg
  * package.json

*To do*

## Configurar los development.services.yml para desarrollar un tema.

Drupal dispone de una serie de cachés que nos permiten navegar con mayor rapidez y fluidez mejorando los tiempos de carga. Esto está muy bien cuando nuestro proyecto está listo para el público, pero mientras estamos desarrollando nos añade complejidad ya que tendríamos que estar limpiando caché cada dos por tres, por ello tenemos el archivo `web/sites/development.services.yml` donde añadir configuración de cara a la fase de desarrollo.

En concreto, nosotros vamos a capar el sistema de cacheo relacionado con las plantillas Twig, tecnología con la que maquetamos las páginas de nuestro Drupal. Para ello debemos añadir las siguientes líneas dentro de la sección `parameters` del archivo `development.services.yml`.

```yml
twig.config:
  debug: true
  auto_reload: true
  cache: null
```

Quedando nuestro `development.services.yml` tal que así:

```yml
parameters:
  http.response.debug_cacheability_headers: true
  twig.config:
    debug: true
    auto_reload: true
    cache: null
services:
  cache.backend.null:
    class: Drupal\Core\Cache\NullBackendFactory
```

Con esto habilitamos el modo debug, habilitamos la autorecompilación de plantillas Twig y deshabilitamos la caché. Además, una vez habilitado el modo debug de Twig, podremos visualizar en nuestro código fuente las famosas `suggestions` en forma de comentario.

## Utilizando las sugerencias (suggestions) para sobrescribir la estructura y contenido de Drupal.

*To do*

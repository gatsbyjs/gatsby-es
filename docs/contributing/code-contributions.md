---
title: Contribuciones de Código
---

¡La belleza de contribuir con código abierto es que puedes clonar tu proyecto favorito, ejecutarlo localmente y probar experimentos y cambios en tiempo real! Te hace sentir como un mago.

En esta página:

- [Preparación del repositorio](#repo-setup)
- [Creando tus propios plugins y loaders](#creating-your-own-plugins-and-loaders)
- [Haciendo cambios a la Librería de inicio](#making-changes-to-the-starter-library)
- [Contribuyendo con sitios de ejemplo](#contributing-example-sites)
- [Usando Docker para establecer entornos de pruebas](#using-docker-to-set-up-test-environments)
- [Herramientas de Desarrollo](#development-tools)

## Preparación del repositorio

Esta página incluye detalles específicos del núcleo de Gatsby y de su ecosistema.

Para comenzar a configurar el repositorio de Gatsby en tu máquina usando git, Yarn y Gatsby-CLI, consulta la página de [configurando tu entorno local de desarrollo](/contributing/setting-up-your-local-dev-environment/).

Alternativamente, puedes omitir la configuración local y [usar una herramienta de desarrollo en línea](/contributing/using-an-online-dev-environment/).

Para contribuir al blog o al sitio web Gatsbyjs.org, consulta los pasos de configuración en la página de [contribuciones del blog y sitio web](/contributing/blog-and-website-contributions/). Para instrucciones relativas a la contribución de documentos, visita la [página de contribuciones de documentos](/contributing/docs-contributions/).

## Creando tus propios plugins y loaders

Si creas un loader o plugin, nos encantaría que lo hicieras como código abierto y lo subieras a npm. Para obtener más información sobre la creación de plugins personalizados, consulta la documentación de [plugins](/docs/plugins/) y la [especificación de la API](/docs/api-specification/).

## Haciendo cambios a la Librería de inicio

Nota: No es necesario que sigas estos pasos para enviar una librería de inicio. Esto sólo es necesario si quieres contribuir con funcionalidades de la propia librería de inicio. Para enviar un inicializador, [sigue estos pasos en su lugar](/contributing/submit-to-starter-library/).

Para desarrollar en la librería de inicio, deberás disponer de un token de acceso personal de GitHub.

1. Crea un token de acceso personal en tu GitHub [Ajustes de Desarrollador](https://github.com/settings/tokens).
2. En tus nuevos ajustes de token, garantízale alcance al "public_repo".
3. Crea un archivo en la raíz de tu `www` llamado `.env.development`, y añade el token de esta manera:

```text:title=.env.development
GITHUB_API_TOKEN=AQUI_TU_TOKEN
```

El archivo `.env.development` es ignorado por git. Tu token nunca debería enviarse en tus commits.

## Contribuyendo con sitios de ejemplo

La política de Gatsby es que "Usar" sitios de ejemplo (como los de [ejemplos pertenecientes al repositorio](https://github.com/gatsbyjs/gatsby/tree/master/examples)) debería sólo incluir plugins mantenidos por el equipo principal ya que sinó nos es difícil mantener las cosas actualizadas.

Para contribuir con tus propios sitios de ejemplo, es recomendable crear tu repositorio de Github y enlazarlo ahí con tu plugin fuente, etc.

## Usando Docker para establecer entornos de pruebas

Debido a las diferentes integraciones posibles de Gatsby, puede ayudar lanzar un contenedor Docker con la aplicación de software que necesitas probar. Esto facilita la instalación, por lo que puedes centrarte menos en la configuración y más en los detalles de integración que te interesen.

> ¿Tienes alguna configuración que no esté listada aquí? Háznoslo saber añadiéndola a este archivo y abriendo una PR.

### Docker, Wordpress y Gatsby

Para instalar Wordpress con Gatsby, este archivo `docker-compose.yml` te puede ser de utilidad:

```yaml:title=docker-compose.yml
version: "2"

services:
  db:
    image: mysql:5.6
    container_name: sessions_db
    ports:
      - "3306:3306"
    volumes:
      - "./.data/db:/var/lib/mysql"
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    image: wordpress:latest
    container_name: sessions_wordpress
    depends_on:
      - db
    links:
      - db
    ports:
      - "7000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_PASSWORD: wordpress
    volumes:
      - ./wp-content:/var/www/html/wp-content
      - ./wp-app:/var/www/html

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: sessions_phpmyadmin
    environment:
      - PMA_ARBITRARY=1
      - PMA_HOST=sessions_db
      - PMA_USER=wordpress
      - PMA_PASSWORD=wordpress
    restart: always
    ports:
      - 8080:80
    volumes:
      - /sessions
```

Usa los contenidos del archivo de arriba cuando sigas las instrucciones de instalación de Docker Wordpress: https://docs.docker.com/compose/wordpress/

Usando Docker Compose, puedes iniciar y parar una instancia de Wordpress e integrarla con el [plugin fuente de Gatsby Wordpress](/docs/sourcing-from-wordpress/).

## Herramientas de Desarrollo

### Debugeando el proceso de build

Consulta la página de [Debugeando el proceso de build](/docs/debugging-the-build-process/) para aprender cómo debugear Gatsby.

## Feedback

En cualquier momento durante el proceso de contribución, ¡al equipo de Gatsby Core le encantaría ayudar! ¡Organizamos un [meeting semanal de Mantenedores principales](/contributing/community#core-maintainers-meeting) dónde puedes compartir tus creaciones y recibir consejo y feedback directamente del equipo!

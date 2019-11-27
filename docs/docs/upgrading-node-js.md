---
title: Actualizando tu versión de Node.js
---

## Política de soporte de Node.js de Gatsby

Gatsby apunta a dar compatibilidad con cualquier versión de Node que posea un estado de _Actual (Current)_, _Activa (Active)_, o en _Mantenimiento (Maintenance)_. Una vez que una versión mayor de Node alcanza su estado de _Fin de ciclo (End of Life)_ Gatsby dejará de dar soporte a esa versión.

Gatsby dejará de dar soporte al lanzamiento de Node en _Fin de Ciclo (End of Life)_ en una versión menor.

Revisa el [Documento de lanzamientos de Node](https://github.com/nodejs/Release#nodejs-release-working-group) para ver los estado de las versiones.

## ¿Qué versión de Node poseo?

Ejecuta `node -v` en una ventana de la terminal para ver qué versión de Node posees.

```
node -v
v10.16.0
```

Este ejemplo muestra Node versión 10, específicamente v10.16.0.

## Actualizando desde Node versión 6

Node versión 6 alcanzó el estado de  _Fin de Ciclo (End-of-life)_ el 30 de Abril del 2019. Muchas de las dependencias de Gatsby están actualizándose a Node versión 8 y superiores. Gatsby también debe actualizarse para entregar nuevas funcionalidades y corrección de bugs más rápidamente.

Generalmente recomendaríamos usar [la versión de Node cuyo estado es Activa LTS (Active LTS)](https://github.com/nodejs/Release#nodejs-release-working-group) (Node 10 al momento de escribir esto). De todos modos, en este documento aprenderás cómo actualizar de Node 6 a Node 7 ya que esto probablemente será la actualización menos disruptiva para tí.

> ¿Qué acerca de Node 7? Las versiones estables de Node son lanzamientos con numeros pares - Node 6, Node 8, Node 10, etcétera. Sólo usa los números impares si quieres probar con elementos de vanguardia o experimentales.

Hay múltiples modos de actualizar tu versión de Node dependiendo en cómo lo has instalado originalmente. Léelo para encontrar el mejor enfoque para tí.

### Usando Homebrew

Éste es nuestro modo recomendado de instalar una nueva versión de Node.

Tendrás homebrew instalado en tu computadora si has [seguido la parte cero del tutorial de Gatsby](https://www.gatsbyjs.org/tutorial/part-zero/#-install-nodejs-and-npm). Homebrew es un programa que te permite instalar versiones específicas de Node (y otros programas).

Para actualizar de Node 6 a Node 8 usando Homebrew, abre una ventana de la terminal y ejecuta los siguientes comandos:

```
brew search node
```

Deberías tener un resultado similar a éste:

```
brew search node
==> Formulae
heroku/brew/heroku-node ✔        llnode                           node@10                          nodebrew
leafnode                         node ✔                           node@8                           nodeenv
libbitcoin-node                  node-build                       node_exporter                    nodenv
```

Estás interesado en la versión estable siguiente de Node posterior a Node 6, que es Node 8. Homebrew hace esto disponible en un paquete llamado `node@8`. Ejecuta:

```
brew install node@8
```

Una vez que ésto ha concluido, ejecuta:

```
node -v
```

para confirmar que has actualizado de Node versión 6 a la posterior versión 8 de Node.

### Usando un paquete de administración de versión de Node

Hay dos paquetes populares para administrar múltiples versiones de Node en tu sistema. Utiliza uno de éstos para actualizar a una versión más nueva de Node si ya hay varias disponibles en tu computadora.

Éstos paquetes son muy útiles para personas que trabajan regularmente con distintas versiones de Node.

#### nvm

Ejecuta

```
nvm
```

en una ventana de la terminal para ver si nvm está instalado en tu sistema. Si está instalado, ejecuta:

```
nvm install 8
nvm alias default 8
```

para instalar Node versión 8.

[Revisa la documentación de nvm para más instrucciones](https://github.com/nvm-sh/nvm).

#### n

Ejecuta:

```
n
```

en una ventana de terminal para ver si n está instalado en tu sistema. Si está instalado, puedes ejecutar `n 8` para instalar y usar Node versión 8.

[Revisa la documentación de n para más instrucciones](https://github.com/tj/n).

### Instalando desde  nodejs.org

Si no estás usando alguno de los métodos de instalación listados previamente, puedes [descargar un instalador de Node directamente desde nodejs.org](https://nodejs.org/es/).

El modo recomendado de instalar Node de Gatsby  es utilizando Homebrew. Refiérete a la [sección previa de Homebrew en este documento](#using-homebrew) para más información.

## Conclusión

Gatsby toma la compatibilidad con versiones previas en serio y apunta a dar compatibilidad con versiones anteriores de Node por el mayor tiempo posible. Entendemos que manejar entre distintas versiones de software no es un modo productivo de pasar tu día.

Gatsby también confía en un enorme ecosistema de dependencias de JavaScript. A medida que el ecosistema se aleja de versiones anteriores y ya no compatibles de Node tenemos que mantenernos en velocidad para asegurarnos que los errores puedan ser arreglados y nuevas funcionalidades puedan ser lanzadas.

En éste documento has aprendido cómo actualizar de Node versión 6 (que ha alcanzado el estado de  _Fin de Ciclo (End of Life)_ status), a Node versión 8 (que ha alcanzado el estado de _En Mantenimiento (Maintenance)_.

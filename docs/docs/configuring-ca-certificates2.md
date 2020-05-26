---
title: Configurando Certificados de CA
---

Si usas un registro de paquete privado (generalmente uno corporativo) que requiere un certificado de una CA (autoridad certificada), es posible que deba configurar el certificado en tu configuración de `npm`, `yarn`, y `node`.

## Errores comunes de certificados mal configurados

Si ves errores como `unable to get local issuer certificate` en la salida de la consola al intentar instalar un plugin de Gatsby, una mala configuración del certificado podría ser el problema. Esto ocurre particularmente con los plugins o temas que necesitan ser compilados como un módulo nativo de Node.js (e.g. `gatsby-plugin-sharp`). Puede suceder cuando instalas paquetes de un registro privado (vía `npm install` o `yarn install`) sin una configuración adecuada del certificado.

## opción de configuración cafile

Tanto [npm](https://docs.npmjs.com/misc/config#cafile) como [yarn](https://yarnpkg.com/lang/en/docs/cli/config/), permiten la opción de configuración `cafile`. Tendrás que agregar `cafile` como la clave y configurar la ruta de tu certificado como el valor.

### Usando npm para configurar cafile

```shell
npm config set cafile "path-to-my-cert.pem"
```

Para verificar el valor de la ruta del certificado en la clave `cafile`, usa el siguiente comando para obtener todas las claves que se encuentran en tu configuración npm:

```shell
npm config ls -l
```

### Usando yarn para configurar cafile

```shell
yarn config set cafile "path-to-my-cert.pem"
```

Ahora puedes verificar los valores en tu configuración yarn con el siguiente comando:

```shell
yarn config list
```

### Usando Node.js

Alternativamente, también puedes configurarlo para Node.js en tu máquina. Exporta la ruta de tu certificado con la variable `NODE_EXTRA_CA_CERTS`:

```shell
export NODE_EXTRA_CA_CERTS=["path-to-my-cert.pem"]
```

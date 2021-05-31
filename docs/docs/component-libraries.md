---
title: Crear bibliotecas de componentes
---

Las bibliotecas de componentes a menudo se usan en sistemas de UI basados en componentes como React y Vue. Típicamente son repositorios versionados de componentes.

El [Sistema de Diseño Carbon](https://www.carbondesignsystem.com/) de IMB y el [Blueprint](https://blueprintjs.com/) de Palantir son ambos buenos ejemplos.

## Por qué bibliotecas de componentes

Existen varias razones para crear bibliotecas de componentes.

- **Crear un diseño unificado**. En las grandes propiedades web y aplicaciones web, la apariencia puede diferir en diferentes secciones mantenidas por diferentes equipos. Las bibliotecas de componentes se usan a menudo para implementar un [sistema de diseño](https://www.designsystems.com/).
- **Evita reinventar la rueda**. Las bibliotecas de componentes incluyen elementos comunes como carruseles o menús desplegables para evitar la necesidad de que los equipos individuales vuelvan a re-implementar estos componentes.

## Herramientas y configuraciones de equipo

Las bibliotecas de componentes generalmente son mantenidas por un individuo o un equipo de diseño que actúa como curador; cuando un equipo de sitio web o equipo de características necesita un componente, generalmente está disponible para que lo usen, para que puedan trabajar más rápido.

Las bibliotecas de componentes generalmente se almacenan en un repositorio separado. Las aplicaciones o sitios web individuales especifican en sus dependencias (en `package.json`) qué versión de cada componente están utilizando.

Un inconveniente de usar bibliotecas de componentes es la complejidad adicional de las dependencias de repositorio cruzado.

Por ejemplo, si un desarrollador de características necesita cambiar un componente de la biblioteca, el flujo de trabajo de ese desarrollador generalmente involucra dos pull requests; uno para el repositorio del repositorio de componentes para realizar los cambios, y otro para el repositorio del sitio web para aumentar la versión del componente.

## Diferentes métodos de versiones

Existen dos métodos diferentes para versionar bibliotecas de componentes.

La primera es la versión global en toda la biblioteca de componentes. En cualquier commit, la biblioteca tiene un número de versión (por ejemplo, `30.3.1`). Cualquier commit de actualización de un componente generará el número de versión correspondiente. Tanto _Carbon Design System_ como _Blueprint_ adoptan este método.

El segundo enfoque es versionar cada componente en la biblioteca de componentes. Esto fue utilizado, por ejemplo, [por Walmart.com](https://medium.com/walmartlabs/how-to-achieve-reusability-with-react-components-81edeb7fb0e0) - construyeron su biblioteca de componentes como componentes React, y crearon cada componente como un paquete npm separado y versionado.

Este método permite más granularidad. -- _¿qué sucede si deseas una versión anterior de un componente, pero una versión más nueva de otro?_ -- pero requiere herramientas adicionales para que los flujos de trabajo del desarrollador sean agradables.

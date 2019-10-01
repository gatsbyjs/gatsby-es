---
título: Agregar metadatos de página
---

Si ha ejecutado una [auditoría con Lighthouse] (/ docs / audit-with-lighthouse /), es posible que haya notado una puntuación mediocre en la categoría "SEO". Veamos cómo puedes mejorar esa puntuación.

Agregar metadatos a las páginas (como un título o una descripción) es clave para ayudar a los motores de búsqueda como Google a comprender su contenido y decidir cuándo mostrarlo en los resultados de búsqueda.

[React Helmet] (https://github.com/nfl/react-helmet) es un paquete que proporciona una interfaz de componente React para que administres tu [cabeza de documento] (https://developer.mozilla.org/en- US / docs / Web / HTML / Element / head).

El [complemento de react casco] de Gatsby (/ packages / gatsby-plugin-react-casco /) proporciona soporte directo para los datos de representación del servidor agregados con React Helmet. Usando el complemento, los atributos que agregue a React Helmet se agregarán a las páginas HTML estáticas que Gatsby construye.

### Usando `React Helmet` y` gatsby-plugin-react-helmet`

1. Instale ambos paquetes:

`` `concha
npm install --save gatsby-plugin-react-casco react-casco
`` `

2. Agregue el complemento a la matriz `plugins` en su archivo` gatsby-config.js`.

`` `javascript: title = gatsby-config.js
{
  complementos: [`gatsby-plugin-react-helmet`]
}
`` `

3. Use `React Helmet` en sus páginas:

`` `jsx
importar Reaccionar desde "reaccionar"
importar {Casco} desde "react-casco"

La aplicación de clase extiende React.Component {
  render () {
    regreso (
      <div className = "application">
        {/ * highlight-start * /}
        <Casco>
          <meta charSet = "utf-8" />
          <title> Mi título </title>
          <link rel = "canonical" href = "http://mysite.com/example" />
        </Helmet>
        {/ * punto culminante * /}
      </div>
    )
  }
}
`` `

> 💡 El ejemplo anterior es de [React Helmet docs] (https://github.com/nfl/react-helmet#example). ¡Échales un vistazo para más!

También puede estar interesado en consultar el documento sobre [agregar un componente de SEO] (/ docs / add-seo-component /).
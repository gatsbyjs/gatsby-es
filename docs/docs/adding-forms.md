---
title: Agregando formularios
---

Gatsby está construido encima de React. Así que cualquier cosa que es posible con formularios en React es posible en Gatsby. Detalles adicionales de cómo crear formularios pueden ser encontrados en la [documentación de Formularios en React](https://es.reactjs.org/docs/forms.html)

Comencemos con la siguiente página.

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Esta página Gatsby es un compenente React. Cuando quieres crear un formulario, necesitas almacenar el estado del formulario - lo que el usuario a introducido. Convierte tu componente función (_stateless_) a un componente clase (_stateful_)

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  render() {
    return <div>Hello world!</div>
  }
}
```

Ahora que haz creado un componente clase, puedes agregarle `estado` al componente.

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return <div>Hello world!</div>
  }
}
```

Y ahora puedes agregarle algunos campos de entrada:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input type="text" name="firstName" />
        </label>
        <label>
          Last name
          <input type="text" name="lastName" />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

Cuando un usuario teclea en una caja de entrada, el estado se debe actualizar. Agrega una _prop_ `onChange` para actualizar el estado y agrega una _prop_ `value` para mantener la entrada actualizada con el nuevo estado:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  render() {
    return (
      <form>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

Ahora que tus entradas están funcionando, quieres que suceda algo cuando envíes el formulario. Agrega las _props_ `onSubmit` al elemento del formulario y agrega un `handleSubmit` para mostrar una alerta cuando el usuario envíe el formulario:

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  state = {
    firstName: "",
    lastName: "",
  }

  handleInputChange = event => {
    const target = event.target
    const value = target.value
    const name = target.name

    this.setState({
      [name]: value,
    })
  }

  handleSubmit = event => {
    event.preventDefault()
    alert(`Welcome ${this.state.firstName} ${this.state.lastName}!`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          First name
          <input
            type="text"
            name="firstName"
            value={this.state.firstName}
            onChange={this.handleInputChange}
          />
        </label>
        <label>
          Last name
          <input
            type="text"
            name="lastName"
            value={this.state.lastName}
            onChange={this.handleInputChange}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    )
  }
}
```

Este formulario no hará nada ademas de mostrar al usuario información que recién ha introducido. En este punto, quizás quieras mover este formulario a un componente, enviar el estado del formulario a un servidor _backend_, o agregar una validación mas robusta. También puedes usar las fantásticas librerías de React como [Formik](https://github.com/jaredpalmer/formik) o [Final Form](https://github.com/final-form/react-final-form) para hacer mas rápido tu proceso de desarrollo.

¡Todo esto y mas es posible al usar el poder de Gatsby y el ecosistema React!
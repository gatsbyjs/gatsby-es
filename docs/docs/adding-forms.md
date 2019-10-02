---
title: Agregar formularios
---

Gatsby está construido en la parte superior de React. Así que cualquier cosa que sea posible con una forma React es posible en Gatsby. Encontrará más detalles sobre cómo crear formularios React en la sección [Documentación de formularios React](https://reactjs.org/docs/forms.html) (que pasa a ser construido con Gatsby!)

Comencemos con la siguiente página.

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Esta página de Gatsby es un componente React. Cuando desee crear un formulario, debe almacenar el estado del formulario, lo que el usuario ha ingresado. Convierta su componente de función (sin estado) en un componente de clase (con estado).

```jsx:title=src/pages/index.js
import React from "react"

export default class IndexPage extends React.Component {
  render() {
    return <div>Hello world!</div>
  }
}
```

Ahora que ha creado un componente de clase, puede agregar `state` al componente.

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

Y ahora puede agregar algunos campos de entrada:

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

Cuando un usuario escribe en un cuadro de entrada, el estado debe actualizarse. Añadir un `onChange` para actualizar el estado y agregar un `value` para mantener la entrada actualizada con el nuevo estado:

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

Ahora que sus entradas están funcionando, desea que algo suceda cuando envíe el formulario. Agregue accesorios `onSubmit` al elemento formulario y agregue `handleSubmit` para mostrar una alerta cuando el usuario envíe el formulario:

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

Este formulario no está haciendo nada aparte de mostrar la información de usuario que acaba de introducir. En este punto, es posible que desee mover este formulario a un componente, enviar el estado del formulario a un servidor back-end o agregar una validación sólida. También puede usar fantásticas bibliotecas de formularios React como [Formik](https://github.com/jaredpalmer/formik) o [Formulario final](https://github.com/final-form/react-final-form) para acelerar el proceso de desarrollo.

¡Todo esto es posible y más aprovechando el poder de Gatsby y el ecosistema React!

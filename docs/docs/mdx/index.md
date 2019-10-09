---
El titulo: Agregar de componentes a Markdown con MDX
---

Al escribir contenido en forma larga en Markdown es posible que desee incrustar [componentes](/docs/glossary/#component).
Esto a menudo se consigue o bien escribiendo contenido en JSX o usando plugins que usan una sintáxis especial. 
El primer enfoque no es óptimo porque JSX no es el mejor
el formato para el contenido y lo puede hacer menos tratable a miembros de un equipo. La sintaxis 
personalizada y los plugins son a menudo demasiado inflexibles y no promueven la composición. Si
se encuentra queriendo añadir componentes a su contenido puede usar
`gatsby-plugin-mdx` que es un enchufe de unión de Gatsby para integrar MDX en su proyecto.

## ¿Qué es MDX?

[MDX][mdx] es Markdown para la era de los componentes.
Le permite escribir JSX incrustado dentro de Markdown.
Es una excelente combinación porque permite usar Markdown es ser conciso
Sintaxis (como `# Heading`) para su contenido y JSX para más avanzadas, 
o componentes reutilizables.

Esto es útil en sitios basados en contenido donde desea la capacidad 
de introducir componentes como gráficos o alertas sin tener que 
configurar un complemento. Hace hincapié en la composición sobre la configuración
y realmente brilla con entradas de blog interactivas, documentos de diseño
sistemas o artículos de forma larga con interacciones
inmersivas o dinámicas.

Al utilizar MDX, también puede importar otros documentos MDX y renderizarlos
them como componentes. Esto le permite escribir algo como una página de preguntas frecuentes
página en un solo lugar y reutilizarlo en todo su sitio web.

## ¿Cómo se ve en la práctica?

Importar y la sintaxis de JSX funciona igual que en sus componentes. Este
resulta en una experiencia sin fisuras tanto para desarrolladores como para autores de contenido.
Markdown y JSX se incluyen uno al lado del otro así:

```md
import { Chart } from '../components/chart'

# Aquí hay un gráfico

El gráfico se representa dentro de nuestro documento MDX.

<Chart />
```

## La característica

❤️ **Poderoso**: MDX combina Markdown y JSX sintaxis para encajar perfectamente en
Reaccionar/JSX proyectos basados en.

💻 **Todo es un componente**: Utilizar los componentes existentes dentro de su
MDX y la importación de otros MDX archivos como plain componentes.

🔧 **Personalizar**: Decida qué componente se representa para cada Markdown
element (`{ h1: MyHeading }`).

📚 **Basado en Markdown**: La sencillez y la elegancia del markdown permanece;
Usted interleave JSX sólo cuando desee.

🔥 **Increíblemente veloz**: MDX no tiene tiempo de ejecución, todas la compilación se produce
Durante la etapa de creación.

<GuideList slug={props.slug} />

[mdx]: https://mdxjs.com

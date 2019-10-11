# ¿Cómo contribuir? 🤔

Bienvenido a la documentación en Español de Gatsby, antes que todo muchas gracias por tu interes en contribuir a hacer mas acesible la documentación a nuestro idioma, a continuación te mostramos los enlaces de utilidad y una serie de instrucciones que debes seguir para empezar a contribuir.

## Traduciendo las páginas 

La documentación de Gatsby consiste en una serie de páginas maquetadas mediante Markdown que luego son renderizadas por el mismo Gatsby y son las que consumimos día a día, cada uno de estos archivos `markdown (.MD)` corresponde a una página de la documentación, y por grande o pequeńa que sea se debe traducir, ya el equipo de mantenedores ha realizado este trabajo y realizo una lista de todas las páginas que se deben traducir y tenemos un issue de progreso para hacerle seguimiento, el cual puedes encontrar en el [issue de páginas a traducir](https://github.com/gatsbyjs/gatsby-es/issues/4).

## Pasos para traducir una página

Sabemos que todos quieren contribuir pero debemos mantener un orden en las traducciones, para esto el issue de progreso es de gran ayuda, para poder empezar a traducir sigue estos pasos, por favor **no empieces a traducir si no sigues todos estos pasos, y te asignamos la página**, la idea es que no pierdas preciado trabajo y tiempo si la página ya fue tomada por otro, a veces podemos tardar en asignar, pero por favor ten paciencia:

- **1.-** Ve al [issue de progreso de traducción](https://github.com/gatsbyjs/gatsby-es/issues/4) y revisa que página esta **disponible** y quisieras traducir.
- **2.-** Si ya tienes cual quieres traducir, comenta citando a alguno de los mantenedores @horacioh o @darking360 con la página que quieres traducir y así podemos asignarla.
- **3.-** Espera una respuesta en los comentarios, o bien, revisa que la página que deseas traducir ya tiene tu nombre de usuario al lado entre parentesis: 

    ` - index.md (@horacioh)`. 
    
    De esta forma ya sabes que puedes empezar a traducir.

- **4.-** Empieza a traducir 🎉 Si no sabes como empezar, en la siguiente parte te enseñamos como hacer un `fork` del proyecto, clonarlo y a como abrir tu primer PR.

## Crear un fork, clonar

¿Es tu primera contribución a un proyecto de código abierto? Que genial, y no te preocupes, no es un proceso complicado o tedioso, solo hay una serie de pasos que debes seguir para empezar a traducir y crear tu primera contribución, debes crear un `fork` del proyecto, que significa clonar el proyecto base a tus proyectos, de esta manera evitamos choques no deseados en el contenido oficial. Seguidamente clonaras el proyecto a tu equipo de trabajo para tener todo el código de las páginas para que las abras en tu editor de texto, y finalmente cuando termines de traducir, pódras crear tu primer PR para que lo revisemos 🎉 Parece mucho, pero sigue estas instrucciones:

- **1.-** Para crear un `fork` del proyecto, dirigete a la [página principal de las traducciones en Español](https://github.com/gatsbyjs/gatsby-es) y en la parte superior derecha, veras un botón que dice `fork`, dale click y esto creará un `fork` en tus proyectos personales, al finalizar esto, estarás en una página similar a la de Gatsby, solo que con tu nombre de usuario.
- **2.-** Ahora vas a clonar el proyecto, para esto, justo donde quedaste en el paso anterior dale click a `Clone or download` y eso te dará la direccion de tu repositorio, copiala y ve a tu terminal y ejecuta `git clone <URL_DEL_REPOSITORIO>` pegando el enlace de tu repositorio para clonar.
- **3.-** Ya con el proyecto clonado, abrelo en tu editor de texto y ahora debes crear una rama para trabajar ⚙️

## Crear una rama y hacer commit de tus cambios

Al terminar de clonar el proyecto, estaras trabajando sobre la rama `master` en tu repositorio local, los cambios se deben realizar en una rama aparte ya que `master` con los cambios oficiales ya incluidos en la documentación, para esto solo debes crear una rama, traducir y hacer `commit` de estos cambios:

- **1.-** Crea una nueva rama a partir de la rama `master` ejecutando en tu terminal: `git checkout -b <NOMBRE_DE_LA_RAMA>`, trata de que el nombre de la rama tenga concordancia con lo que estas realizando o traduciendo, por ejemplo: `git checkout -b spanish-tutorial-eight`.
- **2.-** Ya estando en tu rama, abre tu editor de texto favorito y empieza a traducir la página que solicitaste 🚀
- **3.-** Al finalizar de traducir, debes hacer `commit` de estos cambios, esto para que el repositorio los guarde, para esto debes agregar tus cambios ejecutando: `git add <RUTA_A_LA_PAGINA>`, debes agregar la ruta al archivo que modificaste, una forma facil de obtener la ruta es ejecutar `git status` y aparecera en rojo el archivo que modificaste, solo agrega el archivo de la página que cambiaste, nada mas.
- **4.-** Ahora debes agregar un comentario a tu commit, para esto ejecuta: `git commit -m "<MENSAJE>"`, por ejemplo: `git commit -m "Translating tutorial eight. Half page ready"`.
- **5.-** Finalmente es hora de subir tus cambios, para esto baste con ejecutar: `git push origin` o `git push origin <NOMBRE_DE_LA_RAMA>`.
- **6.-** Tus cambios ya estan en tu repositorio en Github, ahora solo resta crear tu PR.

## Creando un PR

Ya todos tus cambios estan en el repositorio, pero no el oficial, para poderlos incluir debes crear un PR y los mantenedores lo revisarán para aprobarlo, esto para comprobar que tiene los números de línea correctos, acentos y gramática, sigue estos pasos:

- **1.-** Ve a los [issues del proyecto](https://github.com/gatsbyjs/gatsby-es/pulls) y haz click en el botón `New pull request`.
- **2.-** Como tus cambios están en tu repositorio que es un `fork` del oficial, debes hacer click en el enlace que dice: `compare across forks`.
- **3.-** En las opciones de la derecha, debes seleccionar tu repositorio, usualmente aparece como: `<TU_NOMBRE_DE_USUARIO>/gatsby-es`, y al lado debes seleccionar al nombre de la rama en la que estan tus cambios.
- **4.-** Ahora se mostrarán los cambios que realizaste en el código, si todo se ve bien, haz click en `Create pulll request`.
- **5.-** Ahora se te pedirá un titulo para el PR y unos comentarios, agrega un titulo acorde con tu traducción o cambios, y un comentario explicando los mismos, y dale a `Create pull request`.
- **6.-** Ahora agregarás la etiqueta `Work in progress` a tu PR, puedes hacer esto en las opciones de la mano derecha del PR, dale click a `Labels` y busca esta etiqueta, asi sabremos que sigues trabajando en el PR. Al terminar con tu trabajo, cambia la etiqueta a `Ready for review` para que sepamos que ya esta listo para ser evaluado.
- **7.-** Los mantenedores revisarán tus cambios, y te harán saber si hay correcciones o se puede pasar directo, de existir correcciones, solo debes agregarlas, volver a hacer commit de tus cambios y subir a tu repositorio, el PR se actualizará automáticamente 🧙

## Recomendaciones al trabajar en las traducciones

Puedes encontrar más detalle sobre el estilo que deben llevar las traducciones en la [guía de estilos y glosario](https://github.com/gatsbyjs/gatsby-es/blob/master/TRANSLATION.md), pero aquí agregamos los detalles mas importantes que debes tener en cuenta al traducir que pueden parecer basicos pero son de suma importancia:

- Cuida tu ortografía, es importante que la documentación tenga una buena ortografía tanto acentos como palabras bien escritas, siempre ten cuidado con esto.
- No agregues o elimines líneas de la documentación, traduce siempre sobre las mismas líneas, una forma fácil de comprobar esto es revisar que las primeras y últimas 10 líneas de la página tengan contenido igual o títulos, pero por supuesto traducidos.
- Siempre manten un Español neutral, no uses palabras que estén influenciadas por tu región o país, esto sera evaluado mas adelante por los mantenedores pero es de gran ayuda para mantener la documentación con un lenguaje neutral.
- Si no conoces la traducción a una palabra puedes utilizar herramientas como [Google translate](https://translate.google.com/?hl=es), no hay nada de malo en esto, pero no traduzcas una página completa con este ya que el significado se puede perder.

Una buena forma de tener en cuenta aspectos como estos es crear una lista de checks en tu PR, por ejemplo:

- [ ] Traducción inicial
- [ ] Comprobar gramática y acentos
- [ ] Leer antes de enviar

## No se inglés, ¿aún así puedo contribuir?

¡Por supuesto que si! Como pudiste leer en la sección arriba de esta, entre los aspectos vitales de las traducciones estan la ortografía y la gramática, los mantenedores hacen su mejor esfuerzo por mantener limpios estos aspectos, pero siempre se les puede escapar algo, tambien puedes contribuir leyendo las traducciones y detectando errores, bien sean estos aspectos o quizás palabras mal escritos, modismos o palabras que no son de Español neutro, puedes ayudarnos a curar este contenido 🤓 Envíanos un PR con correcciones 🚀

## Recompensas ✨

Al contribuir con un proyecto como este no solo estarías contribuyendo a código abierto (lo cual es genial), si no que tambien entras a los contribuidores oficiales de Gatsby, y por si esto no fuera lo suficiente, el equipo de Gatsby te quiere agradecer regalándote un [premio](https://www.gatsbyjs.org/contributing/contributor-swag/) de la [tienda oficial de Gatsby](https://store.gatsbyjs.org/) ❤️ Si sigues contribuyendo puedes optar por más regalos, con 5 contribuciones o más, revisa la [página oficial](https://www.gatsbyjs.org/contributing/contributor-swag/) para más información 🧐

## Extensión de Markdown para VS Code

Al traducir encontrarás sintaxis como `[texto](https://www.google.com)` y muchas otras como `**texto en negrita**`, esto corresponde a sintaxis de Markdown, son archivos que luego son renderizados a texto en nuestras páginas web, una forma excelente de saber si tienes bien escrito el Markdown es hacer una pequeña visualización de este, para no desplegar o ejecutar herramientas tediosas, Visual Studio Code posee una extension para visualizar Markdown, junto a otras herramientas útiles, puedes encontrarlo en [este enlace](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one), si no utilizas este editor, puedes valerte de cualquier extensión que te ayude a esto, solo asegúrate de que el formato y la sintaxis estan bien, por ejemplo, nunca separes `[texto](https://www.google.com)` como `[texto] (https://www.google.com)` ya que esto daña el enlace que debe aparecer allí 🔥

## A traducir 🏃‍

Si has leído hasta aquí, ¿Qué estas esperando?, pide una página que quieras traducir en [este issue](https://github.com/gatsbyjs/gatsby-es/issues/4) y empieza a contribuir con la comunidad de Gatsby ❤️

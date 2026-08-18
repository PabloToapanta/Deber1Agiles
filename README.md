
# Guía de Trabajo Colaborativo: Deber 1 (Metodologías Ágiles)
Formato: Springer Nature LaTeX | Control de versiones: Git & GitHub

---

## 1. Reglas de Oro para Evitar Conflictos en Git

1. **Sincronizar SIEMPRE antes de escribir:**
   ```bash
   git pull origin main

2. **Una oración por línea:**
Presiona `Enter` después de cada punto y seguido. LaTeX une los párrafos automáticamente en el PDF compilado, y esto permite que Git rastree y fusione cambios línea por línea sin generar conflictos de párrafo.
3. **Commits atómicos y descriptivos:**
Sube cambios pequeños y específicos en lugar de un commit gigante al final del día.
4. **División de secciones:**
Procuren no editar la misma sección exacta al mismo tiempo (ejemplo: uno redacta `Introduction` y el otro `Methods`).

---

## 2. Flujo de Trabajo Diario

```bash
# 1. Obtener la última versión del repositorio
git pull origin main

# 2. Realizar tus ediciones en sn-article.tex / sn-bibliography.bib

# 3. Guardar y verificar el estado
git status

# 4. Registrar los cambios
git add .
git commit -m "docs: redactada la seccion de metodologia"

# 5. Enviar cambios a GitHub
git push origin main

```

> **En caso de conflicto al hacer push:**
> Si tu compañero subió cambios antes que tú, Git rechazará el push. Ejecuta:
> ```bash
> git pull --rebase origin main
> # Si hay conflictos, abre el archivo, resuelve las marcas <<<<<< / >>>>>>, guarda y ejecuta:
> git add sn-article.tex
> git rebase --continue
> git push origin main
> 
> ```
> 
> 

---

## 3. Consideraciones con TeXstudio


### Configuración del Motor de Compilación en TeXstudio

Para que la plantilla de Springer compile correctamente con sus referencias:

1. Ve a **Opciones > Configurar TeXstudio > Construir (Build)**.
2. Verifica que las herramientas predeterminadas estén asignadas así:
* **Compilador por defecto:** `PDFLaTeX`
* **Herramienta de bibliografía por defecto:** `BibTeX`


3. Al compilar con bibliografía nueva, el orden de compilación manual es:
* **F6** (PDFLaTeX) $\rightarrow$ **F8** (BibTeX) $\rightarrow$ **F6** (PDFLaTeX) $\rightarrow$ **F6** (PDFLaTeX).
*(O presionar **F5** [Compilación y visualización] dos veces).*



### Manejo de archivos abiertos en TeXstudio

* Si estás editando en TeXstudio y haces un `git pull` en la terminal, TeXstudio detectará el cambio externo y preguntará si deseas **recargar el archivo desde el disco**. Selecciona **Sí/Reload** para no sobreescribir lo que bajaste de GitHub.
* Guarda siempre (`Ctrl + S`) en TeXstudio antes de ejecutar comandos `git add` o `git commit` en la terminal.

---

## 4. Estructura de Archivos del Proyecto

```text
Deber1Agiles/
├── .gitignore            # Ignora archivos basura de compilación
├── README.md             # Guía de trabajo
├── sn-article.tex        # Documento principal (manuscrito)
├── sn-bibliography.bib   # Referencias bibliográficas en formato BibTeX
├── sn-jnl.cls            # Archivo de clase Springer (no modificar)
├── bst/                  # Formatos de estilo bibliográfico
└── fig.eps               # Figuras e imágenes del documento

```
# Conceptos Para manejar Latex
Para trabajar en la plantilla de Springer sin enredarte con el código avanzado, solo necesitas entender cómo se divide el documento y cómo usar los comandos básicos de escritura.

---

**1. Anatomía básica del documento**

El archivo `sn-article.tex` tiene dos grandes bloques:

* **Preámbulo (antes de `\begin{document}`):** Contiene la configuración del formato y paquetes. No toques nada aquí excepto si necesitas agregar un paquete específico.
* **Cuerpo (entre `\begin{document}` y `\end{document}`):** Aquí va todo tu texto, autores, secciones y bibliografía.

---

**2. Datos iniciales: Título, Autores y Resumen**

Busca estos bloques en el archivo y reemplázalos con su información:

```latex
\title[Título Corto]{Título Completo del Trabajo de Metodologías Ágiles}

% Primer autor
\author*[1]{\fnm{Pablo} \sur{Toapanta}}\email{tu_correo@uta.edu.ec}

% Segundo autor
\author[1]{\fnm{NombreCompañero} \sur{ApellidoCompañero}}\email{correo_companero@uta.edu.ec}
\equalcont{Ambos autores contribuyeron por igual a este trabajo.}

% Institución / Universidad
\affil[1]{\orgdiv{Facultad de Ingeniería en Sistemas}, \orgname{Universidad Técnica de Ambato}, \orgaddress{\city{Ambato}, \country{Ecuador}}}

% Resumen y Palabras Clave
\abstract{Aquí escriben el resumen del trabajo en un solo párrafo claro y conciso.}

\keywords{Metodologías Ágiles, Scrum, Git, Control de Versiones}

\maketitle

```

---

**3. Secciones y Jerarquía de Texto**

Para organizar el cuerpo del trabajo, borra el texto de ejemplo de la plantilla y utiliza estos comandos para estructurar sus temas:

```latex
\section{Introducción}\label{sec:intro}
Aquí va el texto de la introducción.
Recuerden escribir una oración por línea para Git.

\section{Metodología}\label{sec:metodologia}
Descripción de la metodología utilizada.

\subsection{Marco de Trabajo Scrum}\label{subsec:scrum}
Detalle de las ceremonias y roles.

\subsection{Gestión de Versiones con Git}\label{subsec:git}
Detalle de las ramas y flujo de trabajo.

\section{Resultados y Discusión}\label{sec:resultados}
Análisis de lo obtenido.

\section{Conclusiones}\label{sec:conclusiones}
Conclusiones finales del deber.

```

---

**4. Comandos esenciales para escribir en LaTeX**

* **Formato de texto:**
* **Negrita:** `\textbf{texto en negrita}`
* *Cursiva:* `\textit{texto en cursiva}`
* Salto de párrafo: Deja **una línea en blanco** en el código para separar dos párrafos.


* **Listas:**
```latex
% Lista con viñetas
\begin{itemize}
    \item Primer punto.
    \item Segundo punto.
\end{itemize}

% Lista numerada
\begin{enumerate}
    \item Paso uno.
    \item Paso dos.
\end{enumerate}

```


* **Imágenes (.png o .jpg):**
Guarda la imagen en la carpeta del proyecto (por ejemplo `arquitectura.png`) e insértala así:
```latex
\begin{figure}[htbp]
    \centering
    \includegraphics[width=0.7\textwidth]{arquitectura.png}
    \caption{Diagrama de arquitectura del flujo de trabajo.}
    \label{fig:arquitectura}
\end{figure}

```


* **Referencias cruzadas (llamar figuras o secciones):**
* Para citar la imagen en el texto: `Como se observa en la Figura~\ref{fig:arquitectura}...`
* Para citar una sección: `Ver Sección~\ref{sec:metodologia}...`



---

**5. Cómo manejar la Bibliografía (`.bib`)**

1. Abre el archivo `sn-bibliography.bib`.
2. Borra el contenido de ejemplo y pega tus referencias en formato BibTeX. Por ejemplo:
```bibtex
@book{pressman2014,
  author    = {Roger S. Pressman},
  title     = {Ingeniería del Software: Un Enfoque Práctico},
  year      = {2014},
  publisher = {McGraw-Hill}
}

```


3. Para citar este libro dentro de `sn-article.tex`, usa la clave:
```latex
Según la ingeniería de software tradicional \cite{pressman2014}, los procesos ágiles permiten...

```



---

**6. Secciones finales de la plantilla de Springer**

Al final del documento verás bloques como `\bmhead{Acknowledgements}` o `\section*{Declarations}`. Si su docente no les exige estas secciones para el deber académico, pueden comentarlas anteponiendo `%` a cada línea o simplemente borrarlas, dejando únicamente:

```latex
\bibliography{sn-bibliography}
\end{document}

```

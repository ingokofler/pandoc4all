# Examples

## PlantUML Integration

PlantUML diagrams can be integrated directly within Markdown files.
Pandoc will invoke a dedicated PlantUML filter to render the PlantUML code
to an image which is finally included in the PDF.

More details can be found in the offical documentation of the filter ([Link](https://github.com/timofurrer/pandoc-plantuml-filter)).

> **_NOTE:_** Using the integration requires the extra paramters `--filter pandoc-plantuml` on the command line.

### How to run - Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           plantuml-integration.md `
           -o plantuml-integration.pdf `
           --filter pandoc-plantuml
```

#### How to run - Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           plantuml-integration.md \
           -o plantuml-integration.pdf \
           --filter pandoc-plantuml
```

## Included Eisvogel Template

The image comes with the [Eisvogel Pandoc Latex](https://github.com/Wandmalfarbe/pandoc-latex-template) template for rendering.
See the [Examples](https://github.com/Wandmalfarbe/pandoc-latex-template/tree/master/examples) on what can be achieved with this template. Of course
this template can be combined with the Plant UML support.
Note that the stylesheet can be parametrized based on the available
[Custom Template Variables](https://github.com/Wandmalfarbe/pandoc-latex-template#custom-template-variables).


The most recent template is located in the image at `/opt/eisvogel/eisvogel.tex`.
One can inspect the file `/opt/eisvogel/version` to check for the included
version.

### How to run - Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           assignment-using-eisvogel.md `
           -o assignment-using-eisvogel.pdf `
           -V header-center="PLF" `
           --listings `
           --template eisvogel.tex `
           --filter pandoc-plantuml
```

### How to run - Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           assignment-using-eisvogel.md \
           -o assignment-using-eisvogel.pdf \
           -V header-center="PLF" \
           --listings \
           --template eisvogel.tex \
           --filter pandoc-plantuml
```

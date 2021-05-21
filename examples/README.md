# Examples

## PlantUML Integration

PlantUML diagrams can be integrated directly within Markdown files.
Pandoc will invoke a dedicated PlantUML filter to render the PlantUML code
to an image which is finally included in the PDF.

More details can be found in the offical documentation of the filter ([Link](https://github.com/timofurrer/pandoc-plantuml-filter)).

> **_NOTE:_** Using the integration requires the extra paramters `--filter pandoc-plantuml` on the command line.

## How to run the examples

Invocation shown based on the example `plantuml-integration.md`.

Windows Powershell

```powershell
docker run -it -v C:\your\path\here\examples:/data `
           pandoc4all `
           plantuml-integration.md `
           -o plantuml-integration.pdf `
           --filter pandoc-plantuml
```

Linux

```shell
docker run -it -v /your/path/here/examples:/data \
           pandoc4all \
           plantuml-integration.md \
           -o plantuml-integration.pdf \
           --filter pandoc-plantuml
```

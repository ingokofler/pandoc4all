FROM pandoc/latex

ENV PLANTUML_VERSION=1.2021.4
ENV EISVOGEL_VERSION=1.6.0

# python3 py3-pip                 ... for pandoc plantuml filter
# openjdk11-jre-headless graphviz ... for plantuml
# fontconfig freetype ttf-dejavu  ... for plantuml as well
RUN apk add --no-cache python3 py3-pip openjdk11-jre graphviz fontconfig freetype ttf-dejavu

# install pandoc-plantuml-filter via pip3
RUN pip3 install pandoc-plantuml-filter

# download specified version of plantuml
RUN mkdir -p /opt/plantuml && \
    wget -O /opt/plantuml/plantuml.jar http://sourceforge.net/projects/plantuml/files/plantuml.${PLANTUML_VERSION}.jar/download

# pandoc filter requires the existence of such a script
ADD plantuml /usr/bin/plantuml
RUN chmod a+x /usr/bin/plantuml

# download and integrate eisvogel template
RUN mkdir -p /opt/eisvogel && \
    echo "${EISVOGEL_VERSION}" >/opt/eisvogel/version \
    wget -O /opt/eisvogel/eisvogel.tex "https://raw.githubusercontent.com/Wandmalfarbe/pandoc-latex-template/v${EISVOGEL_VERSION}/eisvogel.tex"
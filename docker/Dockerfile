FROM pandoc/latex

ENV PLANTUML_VERSION=1.2021.4
ENV REVEALJS_VERSION=4.1.0

# python3 py3-pip                 ... for pandoc plantuml filter
# openjdk11-jre-headless graphviz ... for plantuml
# fontconfig freetype ttf-dejavu  ... for plantuml as well
RUN apk add --no-cache python3 py3-pip openjdk11-jre graphviz fontconfig freetype ttf-dejavu

# install pandoc-plantuml-filter via pip3
RUN pip3 install pandoc-plantuml-filter

# download specified version of plantuml
RUN mkdir -p /opt/plantuml && \
    wget -O /opt/plantuml/plantuml.jar http://sourceforge.net/projects/plantuml/files/plantuml.${PLANTUML_VERSION}.jar/download

# download and extract specified version of reveal.js
RUN mkdir -p /opt && \
    wget -O /opt/reveal.js.zip https://github.com/hakimel/reveal.js/archive/refs/tags/${REVEALJS_VERSION}.zip && \
    unzip /opt/reveal.js.zip -d /opt && \
    rm /opt/reveal.js.zip && \
    mv /opt/reveal.js-${REVEALJS_VERSION} /opt/reveal.js

# pandoc filter requires the existence of such a script
ADD plantuml /usr/bin/plantuml
RUN chmod a+x /usr/bin/plantuml

# automatically add revealjs-url as variable to pandoc
ENTRYPOINT ["/usr/local/bin/pandoc", "-V", "revealjs-url:/opt/reveal.js"]

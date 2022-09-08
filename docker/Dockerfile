FROM pandoc/latex

ENV PLANTUML_VERSION=1.2022.6
ENV REVEALJS_VERSION=4.3.1
ENV EISVOGEL_VERSION=1.6.1

# python3 py3-pip                 ... for pandoc plantuml filter
# openjdk11-jre-headless graphviz ... for plantuml
# fontconfig freetype ttf-dejavu  ... for plantuml as well
# make                            ... for the thesis project
RUN apk add --no-cache python3 py3-pip openjdk11-jre graphviz fontconfig freetype ttf-dejavu make

# some of the pandoc packages require psutil - so install/uninstall all the stuff just to build it
RUN apk add --no-cache gcc python3-dev musl-dev linux-headers && \
    pip3 install psutil && \
    apk del gcc python3-dev musl-dev linux-headers

# install pandoc-plantuml-filter and other packages via pip3
RUN pip3 install pandoc-plantuml-filter pandoc-eqnos pandoc-tablenos pandoc-secnos pandoc-fignos pandoc-shortcaption

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

# add additional tex packages for Eisvogel template
# taken from https://github.com/rstropek/pandoc-latex/blob/master/Dockerfile
RUN tlmgr update --self && \
    tlmgr install \
    merriweather \
    fontaxes \
    mweights \
    mdframed \
    needspace \
    sourcesanspro \
    sourcecodepro \
    titling \
    ly1 \
    pagecolor \
    adjustbox \
    collectbox \
    titlesec \
    fvextra \
    pdftexcmds \
    footnotebackref \
    zref \
    fontawesome5 \
    footmisc \
    sectsty \
    truncate \
    tocloft \
    wallpaper \
    morefloats \
    siunitx \
    threeparttable \
    makecell \
    bbold \
    cleveref \
    multirow \
    forloop \
    lipsum \
    courier \
    koma-script \
    mathtools \
    pdfpages \
    lineno

# download and integrate eisvogel template
RUN mkdir -p /opt/eisvogel && \
    echo "${EISVOGEL_VERSION}" >/opt/eisvogel/version && \
    wget -O /opt/eisvogel/eisvogel.tex "https://raw.githubusercontent.com/Wandmalfarbe/pandoc-latex-template/v${EISVOGEL_VERSION}/eisvogel.tex" && \
    mkdir -p /root/.local/share/pandoc/templates && \
    cp /opt/eisvogel/eisvogel.tex /root/.local/share/pandoc/templates/eisvogel.tex

# automatically add revealjs-url as variable to pandoc
ENTRYPOINT ["/usr/local/bin/pandoc", "-V", "revealjs-url:/opt/reveal.js"]

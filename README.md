# Labeling System Docs

This repository provides the documentation for the Labeling System build using Read The Docs. Run `make html` to get a final version in the `/build/html` folder.

## Setup

* [getting started](https://docs.readthedocs.io/en/latest/getting_started.html)
* install python
  * https://www.python.org/downloads/
  * http://www.sphinx-doc.org/en/stable/install.html
* write python in PATH variable (Umgebungsvariaben)
* test in cmd `> python`
* install pip command `> python get-pip.py` [get file](https://bootstrap.pypa.io/get-pip.py)
  * pip has been contained in the Python official installation after version of Python-3.4.0 or Python-2.7.9.
* install sphinx with pip `> pip install sphinx`
* test in cmd `> sphinx-build -h`
* install sphinx autobuild `> pip install sphinx sphinx-autobuild`
* install markdown support `> pip install recommonmark`
* install theme `> pip install sphinx_rtd_theme`

## Rund and Build

* go to git folder with rtd content in cmd `> cd de`
  * clear: `make clean`
  * create: `make html`

## Credits

```
Florian Thiery M.Sc.
- Institut für Raumbezogene Informations- und Messtechnik (i3mainz)
- Römisch-Germanisches Zentralmuseum, Leibniz-Forschungsinstitut für Archäologie (RGZM)
- Mainzer Zentrum für Digitalität in den Geistes- und Kulturwissenschaften (mainzed)
```

## License

MIT License

Copyright (c) 2017 Florian Thiery M.Sc., mainzed

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

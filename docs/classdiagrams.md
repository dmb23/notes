# Class Diagrams in Python

Sometimes I would like to look at class diagrams, and not scroll through my code.
What I just learned: `pylint` actually ships with [pyreverse](https://pylint.pycqa.org/en/stable/pyreverse.html) to do just that:

```bash
pyreverse -o <FORMAT>  my_package[.my_module] -d <OUTPUT_DIRECTORY>
```

creates class diagrams in `dot`, PlantUML `puml` and MermaidJS `mmd` (or anything `graphviz` can handle). For a quick look, it is e.g. possible to create a skeleton with `pyreverse`, copy this (`cat classes.mmd | pbcopy`) into [mermaid.live](https://mermaid.live/) and export what you want to show.

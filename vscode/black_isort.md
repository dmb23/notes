# Use black and isort together in VS Code

VS Code only uses a single formatter at a time. (Also I don't know if import ordering technically counts as a formatter) So there is some additional config needed, to make both happen on save:

This must be changed in `settings.json`:
```json
{
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
        "soure.organizeImports": true
    }
}
```

Of course, set `profile=black` in some isort config (e.g. `pyproject.toml`)

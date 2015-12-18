# Adding themes (optional)

Lets say you want to add a new theme, in example the **material** theme.

Add the theme submodule to themes folder

```bash
git submodule add https://github.com/quokkaproject/theme_material themes/material
git submodule init
```

Create the mapping adding "./themes/material:/quokka/quokka/themes/material" to volumes in docker-compose.yml

```yaml
    volumes:
        ...
        - ./themes/material:/quokka/quokka/themes/material

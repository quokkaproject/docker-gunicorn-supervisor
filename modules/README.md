## Adding modules (optional)

The same process as adding a theme, lets say you want to add **quokka-cart** module.

Add the module submodule

```bash
git submodule add https://github.com/quokkaproject/quokka-cart modules/cart
git submodule init
```

Create the mapping

```yaml
    volumes:
        ...
        - ./modules/cart:/quokka/quokka/modules/cart
```

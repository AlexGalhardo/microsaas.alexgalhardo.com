## Prettier VueJS Templates

- <https://stackoverflow.com/questions/54160676/prettier-to-format-vue>

- Easier is to install vetur octref.vetur extension and then add a .vscode>settings.json with following

```json
{
    "editor.defaultFormatter": "octref.vetur",
    "vetur.format.defaultFormatter.html": "prettier",
    "vetur.format.defaultFormatter.css": "prettier",
    "vetur.format.defaultFormatter.postcss": "prettier",
    "vetur.format.defaultFormatter.scss": "prettier",
    "vetur.format.defaultFormatter.less": "prettier",
    "vetur.format.defaultFormatter.stylus": "stylus-supremacy",
    "vetur.format.defaultFormatter.js": "prettier",
    "vetur.format.defaultFormatter.ts": "prettier"
}
```

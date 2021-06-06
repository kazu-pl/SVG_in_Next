# SVG as ReactComponent in Next:

1 - install the right extension: `yarn add babel-plugin-inline-react-svg -D`

2 - create a `.babelrc` file in root dir and paste:

```
{
  "presets": ["next/babel"],
  "plugins": ["inline-react-svg"]
}
```

3 - then you can import svg files as:
`import File from '../assets/logo.svg';`

- you dont have to write `import { ReactComponent as Logo } from ...` like in CRA
- you can't use absolute paths

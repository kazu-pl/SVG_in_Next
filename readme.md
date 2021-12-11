# There are 2 methods on how to add ability to use SVG as ReactComponents (like in Create React App) in Next

# Method 1 - config with next.config.js - (PREFFERED):

1 - `yarn add @svgr/webpack --dev`

2 - `yarn add url-loader --dev`

3 - create `next.config.js` file in root dir and paste:

```
module.exports = {
  webpack(config) {
    config.module.rules.push({
      test: /\.svg$/,
      //// in early 2021 issuer object worked fine but since 11 dec 2021 it throws an error. You can disable this option and it still works fine.
      // issuer: {
      //  test: /\.(js|ts)x?$/,
      // },
      use: ["@svgr/webpack", "url-loader"],
    });

    return config;
  },
};
```

4 - create file with svg type declarations, for example: `types/svg.d.ts` and paste:

```

declare module "*.svg" {
  export const ReactComponent: React.FunctionComponent<
    React.SVGAttributes<SVGElement>
  >;
  const content: string;
  export default content;
}

```

5 - make sure that in `tsconfig.json` you have included that `next.config.ts` file like: `"include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", "next.config.js"]`

6 - now you can use it just like in Create React App:

```
import LogoURL, { ReactComponent as LogoComp } from "assets/logo.svg";


<LogoComp width={150} />
 <img src={LogoURL} alt="" />
```

---

# Method 2 - simplier and shorter:

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

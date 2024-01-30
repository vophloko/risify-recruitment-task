# Project

In order to list stories of the Button component run the following commands:

```sh
npm install
npm run story:build
npm run story:preview
```

If you'd like to use `volta` there's a specific node version pinned to `package.json`, so go ahead.

To make this component completely typesafe I would need to refactor. The recommended way of extending router-link is to use @ts-ignore on destructured RouterLink props. This sucks and I won't do it.

Also I stick with vanilla CSS because styling method is not specified in the task. Using f.e. Tailwind is a commitment compared to `cva` that could be replaced.

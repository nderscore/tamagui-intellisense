# `nandorojo-tamagui-intellisense`

A VSCode extension for autocompleting Tamagui styles.

<video src="https://user-images.githubusercontent.com/13172299/258659477-90e5faef-df4a-49d9-a647-3f1b2406bda0.mp4">

## Setup

After installing the extension, add `.vscode/settings.json` in your repo with the following:

```json
{
  "nandorojo-tamagui.configPath": "./path-to/tamagui.config.ts"
}
```

Replace that with the relative path to your tamagui config file from the root of your repo. Defaults to `./tamagui.config.ts`.

## Contribute

Clone the GitHub repo, then install dependencies.

```
git clone https://github.com/nandorojo/tamagui-intellisense.git
yarn
```

Then see the [./vsc-extension-quickstart.md](./vsc-extension-quickstart.md) for how to run the extension in VSCode. Below is essentially what you'll do.

Start the dev server in VSCode by Pressing `F5` (or `fn` + `F5` on Mac). It should open a new window for testing. In that window, you should create a folder (let's say `test-folder`) with a tamagui config in it.

- `test-folder/tamagui.config.ts`

```ts
import { shorthands } from "@tamagui/shorthands"
import { themes, tokens } from "@tamagui/themes"
import { createFont, createTamagui } from "tamagui"

export default createTamagui({
  themes,
  tokens,
  shorthands,
})
```

- `test-folder/test.ts`

```ts
declare function styled(a: any, obj: { bg?: string }): any
const View = 1

styled(View, {
  bg: "$",
})
```

And try the autocomplete there.

### Development

When you make changes in `src/server.js`, you have to click the little green refresh at the top of your main VSCode window to see them update in the test window.

This could probably be fixed with a watch script but I haven't done it. The reason: Webpack bundles everything in `dist` in one file, but we're referencing the `server.js` file in `client.ts` which won't get resolved post-build if we use TS. So we have to restart the server to see changes.

In your test window, put a `tamagui.config.ts` in the root to make it simple.

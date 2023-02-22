# doc-gen
Satori + animation + html + tailwind + nix + command line + markdown + diff

- Markdown Runner
- Better Syntax
- Blog Utils

# Markdown runner

# Problem of writing tech blog / docs

## Prone to human error
Running command and writing code on local machine,
then manually copy and paste the command to markdown is prone to error.

## Not (easily) reproducible
- Dependecies might not be specified
  - Dependecies might be updated

Solution: run it automatically

# Problem of automatically running Readme.md

Installing dependencies just for the sake of writing blog will polute our local environment

Managing different dependencies for each post is hard

Each blog post might have same dependency with different versions

# Features

## [Shiki](https://github.com/shikijs/shiki)
- Can use any theme from vscode
- Can use any language supported on vscode

## [Twoslash](https://www.npmjs.com/package/@typescript/twoslash)
- IDE features on markdown
- Use LSP for all languages

## [Nix](https://github.com/NixOS/nix)
- Manage dependencies
- Can run on mac & linux & Github Actions
  - No "Node.js version I wanted is not instaled on Github Actions" problem
- Runs without (docker) container

### Directory level dependency isolation
Nix can isolate dependencies between directory when combined with [direnv](https://direnv.net/)
- Not polluting your environment
- Can install dependencies per blog post
  - e.g. Node.js 16 on blog post A, Node.js 17 on blog post B
  - Old blog post always run on the environment specified by `flake.nix` on that folder, so the commands won't break

# Run the docs automatically

## Prepare isolated env with flake.nix

Add following file to your blog post directory.
```nix
# flake.nix
{
  outputs = { self, nixpkgs }: with nixpkgs.legacyPackages.x86_64-linux; {
    devShell.x86_64-linux = mkShellNoCC {
      buildInputs = [
        nodejs-18_x
        nodePackages.pnpm
      ];
    };
  };
}
```

## Create Readme.md

Runner will run this commands
```
```cli
pnpm --init
pnpm install typescript
tsc --init
\\```
```

Runner will create logging.ts
```
```ts logging.ts
console.log("hello world")
\\```
```


Runner will update logging.ts
```
```diff logging.ts
- console.log("hello world")
+ console.log("hello people")
\\```
```

## Blog polyfill
dev.to
zenn

## SVG All
Satori

## Low Code
Drag-n-Drop

## Related projects
[runme](https://github.com/stateful/runme)

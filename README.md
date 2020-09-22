# neon-tag-prebuild

> A CLI to rename a [Neon](https://neon-bindings.com) `index.node` to a prebuildify-style file

```
npm install neon-tag-prebuild
```

## Usage

[Neon](https://neon-bindings.com) is great, but its story around publishing modules to npm isn't clear yet. Meanwhile, in node-gyp world, [prebuildify](https://github.com/prebuild/prebuildify) (to produce a release) and [node-gyp-build](https://github.com/prebuild/node-gyp-build) (to consume a release) are really neat solutions to shipping prebuilt native modules.

This tool is meant for producing releases, and will basically just take your Neon project's `./native/index.node` (built by `neon build --release`) and copy it to your project's `./prebuilds` folder, much like `prebuildify` does. Although this tool **only** does that simple copy operation, it makes your life a tiny bit easier to produce releases that contain **prebuilds**.

The file will be copied and named appropriately with *tags*, e.g.

- `./prebuilds/linux-x64/node.abi72.node`

This is useful in a CI environment where you can `neon build` for various architectures and versions of Node.js, then bundle them all together in the same `prebuilds` folder so you can release them in your npm package.

To use this, just call the CLI `neon-tag-prebuild` (e.g. in a CI step) after the `native/index.node` has been built, to copy it to `prebuilds`.

*To consume your module published with prebuilds*, check out [neon-load-or-build](https://github.com/staltz/neon-load-or-build), which is analogous to [node-gyp-build](https://github.com/prebuild/node-gyp-build). That is, it will know how to pick the right `.node` file from the `prebuilds` folder.

## License

MIT

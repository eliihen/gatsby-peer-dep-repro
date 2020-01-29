# Reproduction of peer dep in Gatsby with Yarn 2

> This is a minimal reproduction case showing missing peer dependencies in
> `gatsby-source-graphql`. It is not a complete working example of a gatsby app.

Install yarn 2 if you have not done so already

    npm install -g yarn@berry

Now fetch the repo and install dependencies

    git clone git@github.com:esphen/gatsby-peer-dep-repro.git
    cd gatsby-peer-dep-repro
    yarn

The output will be the following

<details>
  <summary>View output of yarn install</summary>
  <pre>
➤ YN0000: ┌ Resolution step
➤ YN0002: │ gatsby-repro@workspace:. doesn't provide react@^16.4.2 requested by gatsby@npm:2.19.10
➤ YN0002: │ gatsby-repro@workspace:. doesn't provide react-dom@^16.4.2 requested by gatsby@npm:2.19.10
➤ YN0002: │ gatsby-cli@npm:2.8.28 doesn't provide @types/react@>=16.8.0 requested by ink@npm:2.6.0
➤ YN0002: │ gatsby@npm:2.19.10 [5e784] doesn't provide @types/react@^15.0.0 || ^16.0.0 requested by react-hot-loader@npm:4.12.19
➤ YN0002: │ gatsby-source-graphql@npm:2.1.32 [5e784] doesn't provide graphql@^0.11.3 || ^0.12.3 || ^0.13.0 || ^14.0.0 requested by apollo-link@npm:1.2.13
➤ YN0002: │ gatsby-source-graphql@npm:2.1.32 [5e784] doesn't provide graphql@^0.11.0 || ^0.12.0 || ^0.13.0 || ^14.0.0 requested by apollo-link-http@npm:1.5.16
➤ YN0002: │ gatsby-source-graphql@npm:2.1.32 [5e784] doesn't provide graphql@^14.2.0 requested by graphql-tools-fork@npm:8.4.0
➤ YN0000: └ Completed in 0.61s
➤ YN0000: ┌ Fetch step
➤ YN0000: └ Completed in 10.63s
➤ YN0000: ┌ Link step
➤ YN0007: │ core-js@npm:2.6.11 must be built because it never did before or the last one failed
➤ YN0007: │ fsevents@patch:fsevents@npm%3A1.2.11#builtin<compat/fsevents>::version=1.2.11&hash=e8cd9e must be built because it never did before or the last one failed
➤ YN0007: │ gatsby-telemetry@npm:1.1.48 must be built because it never did before or the last one failed
➤ YN0007: │ core-js-pure@npm:3.6.4 must be built because it never did before or the last one failed
➤ YN0007: │ gatsby-cli@npm:2.8.28 must be built because it never did before or the last one failed
➤ YN0007: │ gatsby@npm:2.19.10 [5e784] must be built because it never did before or the last one failed
➤ YN0000: └ Completed in 6s
➤ YN0000: Done with warnings in 17.4s
  </pre>
</details>

Now try starting the development server

    yarn start

After a while it breaks due to missing peer deps

<details>
  <summary>View output of yarn start</summary>
  <pre>
success open and validate gatsby-configs - 0.042s

 ERROR

Error in "/home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/gatsby-source-graphql-virtual-7af779f77b/0/cache/gatsby-source-graphql-npm-2.1.32-7c8946e593-1.zip/node_modules/gatsby-source-graphql/gatsby-node.js": A package is trying to access a peer dependency that should be provided by its direct ancestor but isn't

Required package: graphql (via "graphql/language/visitor")
Required by: apollo-utilities@virtual:d1bf604570ea0e0eddfb16e8c0e8ca9b741b5c2fc60a032de46a785d7ad6dffddb9bb333a792a9dfb89e2813c4f86be0727ab220455d27a2c0ba8143b64bc7a7#npm:1.3.3 (via /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-utilities-virtual-06f209a5f6/0/cache/apollo-utilities-npm-1.3.3-8e73ac22c0-1.zip/node_modules/apollo-utilities/lib/)

Require stack:
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-utilities-virtual-06f209a5f6/0/cache/apollo-utilities-npm-1.3.3-8e73ac22c0-1.zip/node_modules/apollo-utilities/lib/bundle.cjs.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_modules/apollo-link/lib/linkUtils.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_modules/apollo-link/lib/link.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_modules/apollo-link/lib/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c-1.zip/node_modules/graphql-tools-fork/dist/links/createServerHttpLink.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c-1.zip/node_modules/graphql-tools-fork/dist/links/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c-1.zip/node_modules/graphql-tools-fork/dist/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/gatsby-source-graphql-virtual-7af779f77b/0/cache/gatsby-source-graphql-npm-2.1.32-7c8946e593-1.zip/node_modules/gatsby-source-graphql/gatsby-node.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/resolve-module-exports.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/validate.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/load.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/commands/develop.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-cli-npm-2.8.28-11886b3838/node_modules/gatsby-cli/lib/create-cli.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-cli-npm-2.8.28-11886b3838/node_modules/gatsby-cli/lib/index.js
- /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bin/gatsby.js



  Error: A package is trying to access a peer dependency that should be provided by its direct ancestor but isn't
  Required package: graphql (via "graphql/language/visitor")
  Required by: apollo-utilities@virtual:d1bf604570ea0e0eddfb16e8c0e8ca9b741b5c2fc60a032de46a785d7ad6dffddb9bb333a792a9dfb89e2813c4f86be0727ab22045  5d27a2c0ba8143b64bc7a7#npm:1.3.3 (via /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-utilities-virtual-06f209a5f6/0/cache/apoll  o-utilities-npm-1.3.3-8e73ac22c0-1.zip/node_modules/apollo-utilities/lib/)
  Require stack:
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-utilities-virtual-06f209a5f6/0/cache/apollo-utilities-npm-1.3.3-8e73ac22c0-1.z  ip/node_modules/apollo-utilities/lib/bundle.cjs.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_m  odules/apollo-link/lib/linkUtils.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_m  odules/apollo-link/lib/link.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/apollo-link-virtual-d1bf604570/0/cache/apollo-link-npm-1.2.13-6163d464c2-1.zip/node_m  odules/apollo-link/lib/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c  -1.zip/node_modules/graphql-tools-fork/dist/links/createServerHttpLink.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c  -1.zip/node_modules/graphql-tools-fork/dist/links/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/graphql-tools-fork-virtual-b75aa26016/0/cache/graphql-tools-fork-npm-8.4.0-5863863f5c  -1.zip/node_modules/graphql-tools-fork/dist/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/$$virtual/gatsby-source-graphql-virtual-7af779f77b/0/cache/gatsby-source-graphql-npm-2.1.32-7c8  946e593-1.zip/node_modules/gatsby-source-graphql/gatsby-node.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/resolve-module-exports.j  s
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/validate.js  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/load.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/load-plugins/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bootstrap/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/commands/develop.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-cli-npm-2.8.28-11886b3838/node_modules/gatsby-cli/lib/create-cli.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-cli-npm-2.8.28-11886b3838/node_modules/gatsby-cli/lib/index.js
  - /home/espen/workspace/other/gatsby-repro/.yarn/unplugged/gatsby-virtual-1e2515688b/node_modules/gatsby/dist/bin/gatsby.js

  - .pnp.js:21092 Object.makeError
    /home/espen/workspace/other/gatsby-repro/.pnp.js:21092:24

  - .pnp.js:29939 resolveToUnqualified
    /home/espen/workspace/other/gatsby-repro/.pnp.js:29939:35

  - .pnp.js:30032 resolveRequest
    /home/espen/workspace/other/gatsby-repro/.pnp.js:30032:27

  - .pnp.js:30100 Object.resolveRequest
    /home/espen/workspace/other/gatsby-repro/.pnp.js:30100:26

  - .pnp.js:29330 Function.module_1.Module._resolveFilename
    /home/espen/workspace/other/gatsby-repro/.pnp.js:29330:34

  - .pnp.js:29215 Function.module_1.Module._load
    /home/espen/workspace/other/gatsby-repro/.pnp.js:29215:40

  - loader.js:1040 Module.require
    internal/modules/cjs/loader.js:1040:19

  - v8-compile-cache.js:159 require
    [v8-compile-cache-npm-1.1.2-3d189dcf94-1.zip]/[v8-compile-cache]/v8-compile-cache.js:159:20

  - bundle.cjs.js:58 Object.<anonymous>
    [apollo-utilities-npm-1.3.3-8e73ac22c0-1.zip]/[apollo-utilities]/lib/bundle.cjs.js:58:16

  - v8-compile-cache.js:178 Module._compile
    [v8-compile-cache-npm-1.1.2-3d189dcf94-1.zip]/[v8-compile-cache]/v8-compile-cache.js:178:30

  - loader.js:1171 Object.Module._extensions..js
    internal/modules/cjs/loader.js:1171:10

  - loader.js:1000 Module.load
    internal/modules/cjs/loader.js:1000:32

  - .pnp.js:29245 Function.module_1.Module._load
    /home/espen/workspace/other/gatsby-repro/.pnp.js:29245:14

  - loader.js:1040 Module.require
    internal/modules/cjs/loader.js:1040:19

  - v8-compile-cache.js:159 require
    [v8-compile-cache-npm-1.1.2-3d189dcf94-1.zip]/[v8-compile-cache]/v8-compile-cache.js:159:20

  - linkUtils.js:5 Object.<anonymous>
    [apollo-link-npm-1.2.13-6163d464c2-1.zip]/[apollo-link]/lib/linkUtils.js:5:26


not finished load plugins - 0.323s
  </pre>
</details>

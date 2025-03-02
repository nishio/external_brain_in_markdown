
:

```
$ npm audit fix                
npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree
npm ERR! 
npm ERR! Found: type-fest@0.21.3
npm ERR! node_modules/type-fest
npm ERR!   type-fest@"^0.21.3" from ansi-escapes@4.3.2
npm ERR!   node_modules/ansi-escapes
npm ERR!     ansi-escapes@"^4.2.1" from @jest/core@26.6.3
npm ERR!     node_modules/@jest/core
npm ERR!       @jest/core@"^26.6.0" from jest@26.6.0
npm ERR!       node_modules/jest
npm ERR!         peer jest@"^26.0.0" from jest-watch-typeahead@0.6.1
npm ERR!         node_modules/jest-watch-typeahead
npm ERR!         1 more (react-scripts)
npm ERR!       1 more (jest-cli)
npm ERR!     ansi-escapes@"^4.3.1" from jest-watch-typeahead@0.6.1
npm ERR!     node_modules/jest-watch-typeahead
npm ERR!       jest-watch-typeahead@"0.6.1" from react-scripts@4.0.3
npm ERR!       node_modules/react-scripts
npm ERR!         react-scripts@"^4.0.3" from the root project
npm ERR!     2 more (jest-watcher, terminal-link)
npm ERR! 
npm ERR! Could not resolve dependency:
npm ERR! peerOptional type-fest@"^0.13.1" from @pmmmwh/react-refresh-webpack-plugin@0.4.3
npm ERR! node_modules/@pmmmwh/react-refresh-webpack-plugin
npm ERR!   @pmmmwh/react-refresh-webpack-plugin@"0.4.3" from react-scripts@4.0.3
npm ERR!   node_modules/react-scripts
npm ERR!     react-scripts@"^4.0.3" from the root project
npm ERR! 
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force, or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
```


npm v7で`ERESOLVE unable to resolve dependency tree Could not resolve dependency:` - Qiita [https://qiita.com/masato_makino/items/06011fcecc91be583636](https://qiita.com/masato_makino/items/06011fcecc91be583636)

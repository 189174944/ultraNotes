> npm -i --legacy-peer-deps

解决

npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree





`ERESOLVE`与`npm@7`有关的问题很常见，因为npm7.x对某些事情比npm6.x更严格。通常，最简单的解决方法是将`--legacy-peer-deps`标志传递给`npm`(e.g.，`npm i --legacy-peer-deps`），或者使用`npm@6`。

如果这不能立即起作用，也许可以先删除`node_modules`和`package-lock.json`。它们将被重新创建。

（提示：使用`npm@6`不需要卸载`npm@7`。使用`npx`指定`npm`的版本。例如：`npx -p npm@6 npm i --legacy-peer-deps`。）
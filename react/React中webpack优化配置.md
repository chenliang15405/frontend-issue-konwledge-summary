# 配置Webpack报错

1. Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead

   extract-text-webpack-plugin还不能支持webpack4.0.0以上的版本。

   解决方式:  `yarn add extract-text-webpack-plugin@next -D`
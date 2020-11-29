## React启动不覆盖tsconfig.json配置文件

> 大坑，create-react-app创建的项目在启动时会自动覆盖`tsconfig.json`中的某些配置

使用create-react-app创建的项目，需要集成typescript，则安装依赖之后，启动项目会自动在项目的根路径下面创建`tsconfig.json`的关于typescript的配置文件，但是对于某些属性，例如`paths`则会在每次启动的时候进行覆盖

### 解决方案

> 在组件中需要引用其他的文件时，一般可以使用相对路径来引用，但是看起来并不是特别好看，而且层级较深的情况下，看起来不是特别优雅，所以可以配置别名的方式来引用文件

- **config-override.js中配置别名**

  > 这里没有指定`npm run eject`，所以采用了`react-app-rewired`的方式来配置webpack

  - 如果没有配置`config-override.js`，则

    ```js
    npm install react-app-rewired --save-dev
    npm install customize-cra --save-dev
    ```

  - 手动在项目根路径下面创建`config-override.js`配置文件

    ```js
    const { override, addWebpackAlias } = require('customize-cra')
    const path = require('path')
    function resolve(dir) {
        return path.join(__dirname, '.', dir)
    }
    
    // 这里覆盖webpack配置，增加路径别名
    module.exports = override(
        //路径别名
        addWebpackAlias({
            '@': path.resolve(__dirname, 'src')
        })
    }
    ```

  - 修改`package.json`

    ```json
    ...
    "scripts": {
        "start": "react-app-rewired start",
        "build": "react-app-rewired build"
    },
    ...
    ```

  `config-override.js`中已经配置了别名

- 创建**paths.json**

  项目根路径下或者指定目录中创建文件

  ```json
  {
      "compilerOptions": {
          "baseUrl": ".",
          "paths": {
              "@/*": ["src/*"]
          }
      }
  }
  ```

  指定typscript中的别名路径

- **tsconfig.json**中配置

  ```json
  {
    "compilerOptions": {
      "target": "es5",
      "allowJs": true,
      "skipLibCheck": true,
      "esModuleInterop": true,
      "allowSyntheticDefaultImports": true,
      "strict": true,
      "forceConsistentCasingInFileNames": true,
      "module": "esnext",
      "moduleResolution": "node",
      "resolveJsonModule": true,
      "isolatedModules": true,
      "noEmit": true,
      "jsx": "preserve",
      "noImplicitAny": false
    },
    "include": [
      "src"
    ],
    "extends": "./paths.json"  // 在这里加上扩展的配置，指定路径
  }
  
  ```

- **使用**

  ```js
  import * from '@/components/home'  // 使用路径别名
  
  ...
  ```

  

启动项目，查看是否正常运行，以及组件是否可以正常导入，一般如果可以正常启动项目，则基本都可以正常运行。




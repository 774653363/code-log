# element-ui 2.x 及 vxe-table 2.x 使用 css 定制主题

### 需求: 客户按照自己的需要，变更页面主题

### 现状：项目使用的是 element-ui 2.x 及 vxe-table 2.x

### 解决方案：

1. 升级 vue3，使用 element-plus + vxe-table 4.x。vue3 之后推荐使用 [css 变量变更主题](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)。肥肠方便，but。对于这个老项目来说升级的代价太重了，承担不起，pass 了。
2. element-ui 2.x 及 vxe-table 2.x 都是推荐使用 scss 生成 css 文件去使用。

   element 有提供[在线主题编辑器](https://element.eleme.cn/#/zh-CN/theme/preview)及其 Chrome 插件，但是没啥用进去就报 500 。

   <img src="attachment:c9e64d075572c2ef3d231acc14f3c2cb" alt="1725460983072.png" style="zoom:50%;" />

   而且有几个 issue 是关于这个问题的，但是没有回应，应该是已经不维护了。

   <img src="attachment:6788f37dc291ce6431b0b2f4bdf720e8" alt="1725461240884.png" style="zoom:50%;" />

   也提供了命令行主题工具 element-theme 去生成，但 install 这个东西需要对 nodejs 版本有要求，还需要安装 python2 的依赖之类的，太恶心了。

   <img src="attachment:edddabb19d71f948ec38b9c0f68d2f31" alt="1725461379396.png" style="zoom:50%;" />

   **基于以上原因，这里建了一个 themeGen 项目，用于在 scss 文件设定主题色，接着使用 sass 命令生成 css 文件。**

   项目依赖如下：
   ```json
   {
     "dependencies": {
       "vxe-table": "2.9.12",
       "element-ui": "^2.15.14"
     },
     "devDependencies": {
       "sass": "~1.32.6"
     }
   }
   ```

   index.scss 案例如下：
   ```scss
   
   // element-ui
   /* 改变主题色变量 */
   $--color-primary: #0283a7;
   @import "./node_modules/element-ui/packages/theme-chalk/src/index";
   
   
   // vxe-table
   @import "./node_modules/vxe-table/styles/variable.scss";
   /* 改变主题色变量 */
   $vxe-primary-color: #0283a7;
   @import "./node_modules/vxe-table/styles/modules.scss";
   
   /* 自定义样式 */
   .test-title {
     color: #0283a7;
     font-size: 18px;
     font-weight: bolder;
   }
   ```

   最后通过 sass 命令生产 css 文件：
   ```
   sass ./index.scss ./index.css --no-source-map
   ```

   最后测试，测试前效果如下：

   <img src="attachment:0b06bf2520c81a96d098c4ba31701049" alt="截图" style="zoom:50%;" />

   上传生成出来的样式文件之后，效果如下：

   <img src="attachment:a2f188c91ccb2f6465b59ac1838af98c" alt="截图" style="zoom:50%;" />

   <br/>

   **最后上代码，[github 地址点这里](https://github.com/774653363/code-log/tree/main/vue/2024090201)。**

<br/>

### 改进：按照这个方法得到的 css 样式。其实还是固定主题的。如果能把 scss 的变量都替换成 css 变量去生成 css 样式，就能实现 vue3 的效果了。

### 参考：[vue2.x element-ui自定义主题 适配css var 变量换肤，真正的自由切换皮肤](https://www.jianshu.com/p/e8d45daee461)

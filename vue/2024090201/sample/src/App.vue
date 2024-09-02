<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />

    <el-divider content-position="center">css 文件上传</el-divider>
    <el-upload
      class="upload-demo"
      drag
      action="#"
      :http-request="upload"
      accept="text/css"
    >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">将文件拖到此处，或<em>点击上传</em></div>
      <div class="el-upload__tip" slot="tip">上传 themeGen 生成的 css</div>
    </el-upload>
    <el-divider content-position="center">element-ui</el-divider>
    <div>
      <el-button>默认链接</el-button>
      <el-button type="primary">主要链接</el-button>
      <el-button type="success">成功链接</el-button>
      <el-button type="info">信息链接</el-button>
      <el-button type="warning">警告链接</el-button>
      <el-button type="danger">危险链接</el-button>
    </div>
    <el-divider content-position="center">vxe-table</el-divider>
    <div>
      <vxe-button content="默认颜色"></vxe-button>
      <vxe-button status="primary" content="主要颜色"></vxe-button>
      <vxe-button status="success" content="成功颜色"></vxe-button>
      <vxe-button status="info" content="信息颜色"></vxe-button>
      <vxe-button status="warning" content="警告颜色"></vxe-button>
      <vxe-button status="danger" content="危险颜色"></vxe-button>
    </div>
    <el-divider content-position="center">custom</el-divider>
    <div class="test-title">这是一个测试的标题</div>
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    upload({ file }) {
      let fr = new FileReader();
      fr.readAsText(file, "UTF-8");

      fr.onload = (e) => {
        const cssContent = e.target.result;

        const styleElement = document.createElement("style");
        styleElement.innerHTML = cssContent;
        document.body.appendChild(styleElement);
      };
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.test-title {
  color: teal;
}
</style>

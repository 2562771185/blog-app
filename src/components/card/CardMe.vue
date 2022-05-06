<template>
  <div class="block" style="border-radius: 10px">
    <el-carousel height="150px" style="border-radius: 10px">
      <el-carousel-item v-for="item in fits" :key="item">
        <img :src="item" :alt="item" style="width: 100%;height: 150px;">
      </el-carousel-item>
    </el-carousel>
  </div>

</template>

<script>
  export default {
    name: 'CardMe',
    data() {
      return {
        fits: ['http://razk1ycbm.hn-bkt.clouddn.com/zouma/1.png', 'http://razk1ycbm.hn-bkt.clouddn.com/zouma/2.png',
          'http://razk1ycbm.hn-bkt.clouddn.com/zouma/6.jpg', 'http://razk1ycbm.hn-bkt.clouddn.com/zouma/5.jpg',
          'http://razk1ycbm.hn-bkt.clouddn.com/zouma/4.jpg'],

      }
    },
    methods: {
      showTool(tool) {
        this.$message({
          duration: 0,
          showClose: true,
          dangerouslyUseHTMLString: true,
          message: '<strong>' + tool.message + '</strong>'
        });
      }
    }
  }
</script>

<style scoped>
  .me-author-name {
    text-align: center;
    font-size: 30px;
    border-bottom: 1px solid #5FB878;
  }

  .me-author-description {
    padding: 8px 0;
  }

  .me-icon-job {
    padding-left: 16px;
  }

  .me-author-tool {
    text-align: center;
    padding-top: 10px;
  }

  .me-author-tool i {
    cursor: pointer;
    padding: 4px 10px;
    font-size: 30px;
  }
</style>

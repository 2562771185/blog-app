<template>
  <div class="block" style="border-radius: 10px">
    <el-carousel height="150px" style="border-radius: 10px" indicator-position="none" interval="300000"@change="musicChange">
      <el-carousel-item v-for="item in fits" :key="item" >
        <img :src="item" :alt="item" style="width: 100%;height: 150px;">
      </el-carousel-item>
    </el-carousel>
    <audio :src="musicSrc" controls="controls"></audio>
  </div>

</template>

<script>
export default {
  name: 'CardMe',
  data() {
    return {
      fits: [
        'http://razk1ycbm.hn-bkt.clouddn.com/musicImgs/%E5%B9%B3%E5%87%A1%E4%B9%8B%E8%B7%AF.webp',
        'http://razk1ycbm.hn-bkt.clouddn.com/musicImgs/%E6%88%91%E6%80%80%E5%BF%B5%E7%9A%84webp.webp',
        'http://razk1ycbm.hn-bkt.clouddn.com/musicImgs/%E7%BA%A2%E6%97%A5.webp'
        , 'http://razk1ycbm.hn-bkt.clouddn.com/musicImgs/%E8%80%81%E7%94%B7%E5%AD%A9.webp',
        'http://razk1ycbm.hn-bkt.clouddn.com/musicImgs/%E5%8D%81%E5%B9%B4.jpg'],
      musics: [
        'http://razk1ycbm.hn-bkt.clouddn.com/music/%E6%9C%B4%E6%A0%91%20-%20%E5%B9%B3%E5%87%A1%E4%B9%8B%E8%B7%AF.mp3',
        'http://razk1ycbm.hn-bkt.clouddn.com/music/%E5%AD%99%E7%87%95%E5%A7%BF%20-%20%E6%88%91%E6%80%80%E5%BF%B5%E7%9A%84.mp3',
        'http://razk1ycbm.hn-bkt.clouddn.com/music/%E6%9D%8E%E5%85%8B%E5%8B%A4%20-%20%E7%BA%A2%E6%97%A5%20%28%E7%B2%A4%E8%AF%AD%29.mp3',
        'http://razk1ycbm.hn-bkt.clouddn.com/music/%E7%AD%B7%E5%AD%90%E5%85%84%E5%BC%9F%20-%20%E8%80%81%E7%94%B7%E5%AD%A9%20%28Live%29.mp3',
        'http://razk1ycbm.hn-bkt.clouddn.com/music/%E9%99%88%E5%A5%95%E8%BF%85%20-%20%E5%8D%81%E5%B9%B4-1.mp3'
      ]
      , musicSrc: ''
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
    },
    musicChange(index){
      this.musicSrc=this.musics[index];
    }
  },
  created() {
    this.musicSrc=this.musics[0];
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

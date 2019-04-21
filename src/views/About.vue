<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div class="block">
      <el-timeline>
        <el-timeline-item v-for="item in data " :timestamp="item" placement="top">
          <el-card>
            <el-button @click="click(item)">{{item}}</el-button>

          </el-card>
        </el-timeline-item>

      </el-timeline>
    </div>
    <div v-for="item in data">

      <button @click="click(item)">{{item}}</button>
      <audio ref="audio" :src="audioSrc" :id="item" title="test"></audio>
    </div>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
@Component({
  components: {
  },
})
export default class About extends Vue {
  public audioSrc: string = '/resource/OperaTicket%20episodeTwo.mp3';
  public data: number[] = [1, 2, 3, 4];
  public click(item) {
    console.log('222');
    (this.$refs.audio[item] as any).currentTime = 60;
    (this.$refs.audio[item] as any).play();
  }
}
</script>

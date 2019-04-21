<template>
    <el-card>
        <el-tag style="margin: 0 10px;width:170px">{{start}}--{{end}}</el-tag>
        <el-button type="primary" @click="play(0.5)">0.5倍数播放</el-button>
        <el-button type="primary" @click="play(1)">正常倍数播放</el-button>
        <el-button type="primary" @click="play(1,true)">循环播放</el-button>
        <el-button type="danger" @click="pause()">暂停播放</el-button>
        <audio :ref="start" :src="audioSrc" :id="start" title="test"></audio>
    </el-card>
</template>
<script lang="ts">
import {Component, Prop, Vue, Watch} from 'vue-property-decorator';
@Component({
    components: {
    },
})
export default class AudioItem extends Vue {
    @Prop() public start!: number;
    @Prop() public end!: number;
    get audioSrc() {
      return `/resource/OperaTicket-episodeTwo.mp3#t=${this.start},${this.end}`;
    }
    public play(playbackRate, loop) {
        const currentAudio = this.$refs[this.start] as any;
        currentAudio.playbackRate = playbackRate;
        currentAudio.loop = loop;
        currentAudio.play();

    }
    public pause() {
        (this.$refs[this.start] as any).pause();
    }
}
</script>

<template>
    <div>
        <el-menu  default-active="1" class="el-menu-demo" mode="horizontal" background-color="#545c64">
            <el-menu-item index="1"><span style="color:#fff">小刘播放器</span></el-menu-item>
        </el-menu>
        <div class="line"></div>
        <el-card shadow="always">
            <p v-for="(item,index) in audio" @click="play(index)" :id="index" class="audio" >{{item}}</p>
        </el-card>
        <audio
                ref="audios"
                :src="audioSrc"
                :preload="audio.preload"
                class="dn"
        />
    </div>


</template>
<script lang="ts">
    import {Component, Vue, Watch} from 'vue-property-decorator';
    import AudioItem from '@/AudioItem.vue'; // @ is an alias to /src
    // import {audio} from '@/plugins/audio';
    import {audio} from '@/plugins/test';

    @Component({
        components: {
            AudioItem,
        },
    })
    export default class Audio extends Vue {
        public audio = audio;
        public start = 0;
        public end = 0;
        // public audioSrc = `/resource/audio.mp3#t=${this.start},${this.end}`;
        public audioSrc = `/resource/19.mp3#t=${this.start},${this.end}`;

        play(time) {
            console.log(time)
            let x:any=document.getElementsByClassName("audio")
            let i;
            for (i = 0; i < x.length; i++) {
                x[i].style.color = "#303133";
            }
            document.getElementById(time).style.color="#3385ff";
            let timeArr = time.split("-");
            this.start = Number(timeArr[0]);
            this.end = Number(timeArr[1]);
            // this.audioSrc = `/resource/audio.mp3#t=${this.start},${this.end}`;
            this.audioSrc = `/resource/19.mp3#t=${this.start},${this.end}`;
            const currentAudio = this.$refs["audios"] as any;
            currentAudio.load()
            console.log(this.start, this.end)
            currentAudio.playbackRate = 1;
            console.log(currentAudio)
            currentAudio.play().then().catch(function(error) {
                console.log('发生错误！', error);
            })
        }


    }
</script>
<style>
    .audio:hover{
        cursor: pointer;
    }

</style>

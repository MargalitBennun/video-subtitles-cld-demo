<template>
  <div class="video-player">

    <video class="video-control" controls>
      <source :src="videoSource" type="video/mp4">
      <source :src="videoSource" type="video/ogg">
    </video>
  </div>
</template>

<script>
  import { VideoSubtitles } from 'VideoSubtitlesCld';
  export default {
      name: 'video-player',
      props: {
      },
      data() {
          return {
              videoPublicId: 'The_Present',
              subtitles: {
                  "subtitles":[
                      {
                          "start-timing":"0:24.8",
                          "end-timing":"0:27.2",
                          "text":"Hey Sweetie! Sorry I got home so late..."
                      },
                      {
                          "start-timing":"0:27.2",
                          "end-timing":"0:30.6",
                          "text":"but I had to pick something up after work."
                      },{
                          "start-timing":"0:30.6",
                          "end-timing":"0:34.4",
                          "text":"It's such a beautiful day outside, you should let some sun inside."
                      },{
                          "start-timing":"0:39.4",
                          "end-timing":"0:42.5",
                          "text":"Why don't you stop playing and open your present?"
                      },{
                          "start-timing":"0:43.1",
                          "end-timing":"0:44.8",
                          "text":"For me?"
                      },{
                          "start-timing":"0:46.2",
                          "end-timing":"0:49.6",
                          "text":"Yes Sir, I don't know why you didn't get the papers."
                      },{
                          "start-timing":"0:55.7",
                          "end-timing":"0:57.7",
                          "text":"Woah! Cool!"
                      },{
                          "start-timing":"1:08.1",
                          "end-timing":"1:10.4",
                          "text":"She's gotta be kidding me!"
                      },{
                          "start-timing":"1:17.5",
                          "end-timing":"1:19.3",
                          "text":"GET LOST!?"
                      },{
                          "start-timing":"3:04.7",
                          "end-timing":"3:07.3",
                          "text":"MUM! WE'LL BE OUTSIDE!"
                      }
                  ]
              },
              subtitlesFile: 'http://127.0.0.1:8082/src/subtitles.json',
              videoSource: 'https://res.cloudinary.com/candidate-evaluation/video/upload/v1545227210/The_Present.mp4'
          };
      },
      created() {
          this.loadVideoWithSubtitles();
      },
      methods: {
          loadVideoWithSubtitles() {
              debugger; // eslint-disable-line
              console.log(VideoSubtitles); // eslint-disable-line
              let myVideoSubtitles = new VideoSubtitles();
              let conf = { videoPublicId: this.videoPublicId };
              if(this.subtitles) {
                  conf.subtitles = this.subtitles;
              } else {
                  conf.subtitlesFile = this.subtitlesFile;
              }
              myVideoSubtitles.addSubtitlesToVideo(conf).then((url)=>{
                  this.videoSource = url;
              });
          }
      },
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .video-player{
    width: 100%;
    height: 100%;
  }
  .video-control {
    width: 50%;
  }
</style>

<template>
  <div class="video-player">
    <h1>Video Subtitles Demo</h1>
    <div class="input-container">
      Video Public ID:  <input type="text" class="video-public-id" :value="videoPublicId" />
    </div>
    <div class="input-container">
        Video Subtitles URL File:  <input type="text" class="video-subtitles-file" :value="subtitlesFile" />
    </div>
    <div class="input-container">
        Video Subtitles JSON:  <textarea  class="video-subtitles" :value="stringifySubtitles"></textarea>
    </div>
    <div class="input-container">
        Video Source:  <span  class="video-subtitles">{{ videoSource }}</span>
     </div>
    <div class="input-container">
      <button class="submit-button" @click="loadVideoWithSubtitles">load subtitles</button>
    </div>
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
              subtitlesFile: 'https://res.cloudinary.com/candidate-evaluation/raw/upload/v1548679237/thepresent_-_subtitles.json',
              videoSource: 'https://res.cloudinary.com/candidate-evaluation/video/upload/v1545227210/The_Present.mp4',
          };
      },
      computed: {
          stringifySubtitles() {
              return JSON.stringify(this.subtitles);
          }
      },
      created() {
          this.loadVideoWithSubtitles();
      },
      methods: {
          loadVideoWithSubtitles() {
              let myVideoSubtitles = new VideoSubtitles();
              let conf = { videoPublicId: this.videoPublicId };
              if(this.subtitles) {
                  conf.subtitles = this.subtitles;
              } else {
                  conf.subtitlesFile = this.subtitlesFile;
              }
              myVideoSubtitles.addSubtitlesToVideo(conf).then((url)=>{
                  this.updateVideoSource(url);
              });

          },
          updateVideoSource(url) {
              this.videoSource = url;
          },
      },
      watch: {
          stringifySubtitles(newValue) {
              this.subtitles = JSON.parse(newValue);
          },
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
  .submit-button {
    background-color: #3203ff;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    cursor: pointer;
  }
  .input-container {
    display: block;
    color: #3203ff;
    text-align: left;
    padding: 10px 10px;
  }
</style>

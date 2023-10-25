<template>
  <!-- eslint-disable -->
  <svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
  <symbol id="check-circle-fill" fill="currentColor" viewBox="0 0 16 16">
    <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.97-3.03a.75.75 0 0 0-1.08.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-.01-1.05z"/>
  </symbol>
  <symbol id="info-fill" fill="currentColor" viewBox="0 0 16 16">
    <path d="M8 16A8 8 0 1 0 8 0a8 8 0 0 0 0 16zm.93-9.412-1 4.705c-.07.34.029.533.304.533.194 0 .487-.07.686-.246l-.088.416c-.287.346-.92.598-1.465.598-.703 0-1.002-.422-.808-1.319l.738-3.468c.064-.293.006-.399-.287-.47l-.451-.081.082-.381 2.29-.287zM8 5.5a1 1 0 1 1 0-2 1 1 0 0 1 0 2z"/>
  </symbol>
  <symbol id="exclamation-triangle-fill" fill="currentColor" viewBox="0 0 16 16">
    <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
  </symbol>
  </svg>



<div class="yt_content">
    <h1 style="text-align: center; margin-top: 50px;" class="yt_hero_text"><b style="color: red">Youtube</b> video downloader</h1>
    <h2 style="text-align: center;">& <br/> Youtube mp4 converter</h2>
    <div class="yt_hero">
      <p>Download your favourite youtube videos <br/> using the video url, its fast and free! 🚀</p>
      <div id="message_box">
      </div>
    </div>

<form class="form-inline my-2 my-lg-0" @submit.prevent="getVideoInfo">

  <div  v-if="errors" class="alert alert-danger d-flex align-items-center" role="alert">
    <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
    <div>
      {{ errors }}
    </div>
  </div>

  <!-- <span v-if="errors"> {{ errors }} </span> -->

        <div class="input_box">
            <input class="yt_search" type="url" placeholder="Enter or paste your video url" @change="getVideoInfo" v-model="videoUrl" required>
            <i style="font-size: large;" class="bi bi-clipboard" @click="pasteLink"></i>
        </div>
        <button class="yt_search_go" type="button" @click="getVideoInfo" :disabled="isLoading">
          <span v-if="isLoading">
            <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
          </span>
          {{buttonMessage}}
        </button>

        <!-- <div id="yt_vid_details" v-if="videoDetails"> -->
        <div id="yt_vid_details">
                <div class="yt_thumb_container" style="width: 100% !important; margin: 0 auto !important; padding: 10px 0px 10px 0px;">
                    <img class="yt_thumbnail" :src="thumbnailUrl" alt="Video Thumbnail">
                </div>
                <h5 id="videoTitle">{{ videoTitle }}</h5>
                <small>Select your preffered download</small>
                <div class="tab_header">
                  <span>Quality</span>
                  <span>size</span>
                  <span>Download</span>
                </div>
                <div class="video-details" v-for="(video, index) in videoDetails" :key="index">
                    <span>{{ video.qualityLabel }}</span>
                    <span>{{ getVideoSize (video.approxDurationMs, video.bitrate) }}</span>
                    <!-- <button @click="downloadVideo(video.url)">download</button> -->
                    <a class="download_btn" :href="video.url" target="_blank" download>
                      download
                      <i style="margin-left: 10px;" class="bi bi-cloud-arrow-down-fill"></i>
                    </a>
                    <!-- {{ video.url }} -->
                </div>
                <div class="video-details audio_only" v-if="audioFile">
                  <span>Audio only</span>
                  <a class="download_btn" :href="audioFile.url" target="_blank" download>
                      download
                      <i style="margin-left: 10px;" class="bi bi-soundwave"></i>
                    </a>
                </div>
        </div>
<div class="yt_audio_details" id="yt_audio_details">
    <div class="audioFormatsList" id="audioFormatsList"></div>
</div>
</form>
</div>

<div class="yt_contents" id="yt_contents">
    <div class="yt_title">Why choose YtubeFetch?</div>
    <p class="yt_content">YtubeFetch is a free online YouTube video downloader that allows you to download videos in a variety of formats and qualities including MP4, AVI.
        It is easy to use and does not require any registration. it also enables users to download subtitles of videos they want to download.
        </p>
    <div class="yt_contents_sub">
        <div class="yt_home_item green">
            <span><i class="bi bi-speedometer2"></i></span>
            <div class="yt_hi_title">Ligthening speed</div>
            <div class="yt_hi_content">Experience the fastest download speeds, ensuring you get your videos in a flash. No more waiting around; tubeFetch accelerates your entertainment.</div>
        </div>
        <div class="yt_home_item blue">
            <span><i class="bi bi-badge-hd-fill"></i></span>
            <div class="yt_hi_title">HD Quality Preservation</div>
            <div class="yt_hi_content">Your favorite videos deserve the best quality. YtubeFetch maintains the high definition of your downloaded content, so you can relish every detail without compromise.</div>
        </div>
            <div class="yt_home_item red">
            <span><i class="bi bi-shield-lock-fill"></i></span>
            <div class="yt_hi_title">Unrestricted Access</div>
            <div class="yt_hi_content">YtubeFetch gives you the freedom to download an array of videos – tutorials, music, vlogs, and more – fostering your personal collection without limitations.</div>
        </div>
    </div>

</div>

<div class="yt_contents">
  <div class="yt_title">Guess what?</div>
   <small style="text-align: center; padding: 10px;">Weve been featured on producthunt, kindly check us out and give us an upvote,and we'd definitely appreciate a kind review</small>
  <a href="https://www.producthunt.com/posts/ytubefetch?utm_source=badge-featured&utm_medium=badge&utm_souce=badge-ytubefetch" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=412169&theme=dark" alt="ytubeFetch - An&#0032;open&#0032;source&#0032;youtube&#0032;video&#0032;downloader&#0032;and&#0032;mp3&#0032;converter | Product Hunt" style="width: 250px; height: 54px;" width="250" height="54" /></a>
</div>

<div class="yt_contents">
    <div class="yt_title" style="text-align: center;" id="FAQ">FREQUENTLY ASKED QUESTIONS (FAQ)</div>

    <div class="yt_contents_sub2">
        <div class="yt_home_item2">

          <div class="accordion" id="accordionExample">
            <div class="accordion-item">
              <h2 class="accordion-header" id="headingOne">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                  <div class="yt_hi_title">How to Download YouTube Videos?</div>
                </button>
              </h2>
              <div id="collapseOne" class="accordion-collapse collapse show" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
                <div class="accordion-body">
                    To download a YouTube video from <a class="yt_link" href="https://ytubefetch.com">YtubeFetch.com</a>, simply follow these steps: <br/>
                    <ol>
                      <li>Copy the url/link of the video you want to download from youtube </li>
                      <li>Go to the <a class="yt_link" href="https://ytubefetch.com">YtubeFetch.com</a> website and paste the URL of the YouTube video you want to download into the search bar and click "Enter".</li>
                      <li>Select the format and quality of the video you want to download.</li>
                      <li>To add subtite to your video, enable the subtitle button.</li>
                      <li>Click on the "Download" button again.</li>
                    </ol>
                </div>
              </div>
            </div>
            <div class="accordion-item">
              <h2 class="accordion-header" id="headingTwo">
                <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false" aria-controls="collapseTwo">
                  <div class="yt_hi_title">What are the supported browsers?</div>
                </button>
              </h2>
              <div id="collapseTwo" class="accordion-collapse collapse" aria-labelledby="headingTwo" data-bs-parent="#accordionExample">
                <div class="accordion-body">
                      Enhance your video downloading experience with YtubeFetch! Our website is optimized to work seamlessly on popular browsers, ensuring you can effortlessly and easily access and download your favorite YouTube videos.
                  Whether you prefer
                  <ol>
                    <li>Chrome <i class="fa fa-chrome" aria-hidden="true"></i></li>
                    <li>Opera Mini <i class="fa fa-opera" aria-hidden="true"></i></li>
                    <li>Safari <i class="fa fa-safari" aria-hidden="true"></i></li>
                    <li>Edge <i class="fa fa-edge" aria-hidden="true"></i></li>
                    <li>Firefox <i class="fa fa-firefox" aria-hidden="true"></i></li>
                  </ol>
                </div>
              </div>
            </div>
          </div>
          <p class="yt_statement">YtubeFetch guarantees compatibility and top-notch performance. Say goodbye to compatibility issues and enjoy hassle-free video downloads with YtubeFetch on your preferred browser.</p>
      </div>

    </div>

</div>

<div v-if=showAd class="adsSpace">
  <span style="position: relative;">
      we can help you <br/> place your adverts here...
      <a>Contact us</a>
      <span class="adsDismisser">&times;</span>
  </span>

</div>

<footer>
  <div class="tiny-group">
    <a class="navbar-brand" href="/"><img src="../assets/logo.png"> YtubeFetch</a>
    <ul class="footer-list-head">
      <li class="footer-list" onclick="showCustomModal()">youtube downloader</li>
      <li class="footer-list" onclick="showCustomModal()">Facebook downloader</li>
      <li class="footer-list" onclick="showCustomModal()">instagram downloader</li>
      <li class="footer-list" onclick="showCustomModal()">twitter downloader</li>
    </ul>
    <div class="yt_tiny_2">
      <a href="TOS.html">Terms of service</a>
      <a href="TOS.html">Privacy Policy</a>
    </div>
    <ul class="footer-list-head">
      <li><a class="yt_whatsapp" href="https://wa.me/+2348156074667">
        <i class="fa fa-whatsapp" aria-hidden="true"></i> whatsapp</a>
      </li>
    </ul>

  </div>
  <div class="yt_footer">&copy; 2023 tubefetch, All rights reserved.</div>
</footer>

</template>

<script>
import axios from 'axios'
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
const apiUrl = 'http://127.0.0.1:8000/api'

export default {
  name: 'HomeView',
  components: { },
  data () {
    return {
      videoUrl: '',
      videoDetails: '',
      buttonMessage: 'Get Video',
      errors: '',
      isLoading: false,
      thumbnailUrl: '',
      videoTitle: '',
      showAd: true,
      audioFile: ''
    }
  },

  methods: {

    async getVideoInfo () {
      try {
        this.buttonMessage = 'getting video...'
        this.isLoading = true

        const response = await axios.get(`${apiUrl}/get-info/`, { params: { vid_url: this.videoUrl } })
        this.videoDetails = response.data.props
        this.thumbnailUrl = response.data.thumbnailUrl
        this.videoTitle = response.data.title
        this.audioFile = response.data.audioOnlyFormats[0]

        console.log(response.data)
        this.buttonMessage = 'Get Video'
        this.isLoading = false
      } catch (error) {
        console.error('Error fetching video info:', error)
        this.errors = 'An error occurred while fetching video info'

        this.isLoading = false
        this.buttonMessage = 'Get Video'
      }
    },

    getVideoSize (approxDurationMs, bitrate) {
      // const sizeInBytes = parseInt(contentLength, 10)
      // const sizeInMB = sizeInBytes / (1024 * 1024)
      // Calculate the video size in bytes
      const durationInMs = parseInt(approxDurationMs, 10)
      const bitrateInBps = bitrate
      const sizeInBytes = (durationInMs / 1000) * (bitrateInBps / 8) // Convert duration from ms to seconds and bitrate from bps to bytes per second

      // Convert the size from bytes to megabytes (MB)
      const sizeInMB = Math.round(sizeInBytes / (1024 * 1024)) // 1 MB = 1024 * 1024 bytes

      return `${sizeInMB} MB`
    },

    pasteLink () {
      if (navigator.clipboard) {
        navigator.clipboard.readText()
          .then(copiedText => {
            this.videoUrl = copiedText
          })
          .catch(error => {
            console.error('Error reading clipboard:', error)
          })
      } else {
        console.error('Clipboard API not supported')
      }
    },

    async downloadVideo (videoUrl) {
      const proxyUrl = 'https://techzone-backend-c28bd32b1555.herokuapp.com'
      console.log('downloading video...')
      try {
        const response = await fetch(proxyUrl + videoUrl, { mode: 'cors' })
        const blob = response.blob()
        const url = window.URL.createObjectURL(blob)
        const a = document.createElement('a')
        a.href = url
        a.download = `ytubefetch.com | ${this.videoTitle}` // You can specify the desired filename here
        document.body.appendChild(a)
        a.click()
        window.URL.revokeObjectURL(url)
      } catch (error) {
        console.error('Error downloading the video:', error)
      }
    }
  }
}
</script>

<style scoped>
.alert{
  font-size: 0.9em;
  text-align: left;
}

.video-details{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 8px 0px;
  border-radius: 5px;
  border: 1px solid #fff;
  padding: 0px 10px;
}

.tab_header > span {
    background: #e1e1e1;
    width: 100%;
    text-align: left;
    padding: 10px;
    border-radius: 5px;
}

.video-details:hover{
  border: 1px solid #efefef;
}
.tab_header{
  color: #000000;
  gap: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 8px 0px;
  border-radius: 5px;
}

.adsSpace{
  border-radius: 10px;
  width: 250px;
  font-size: 12px;
  /* border: 1px solid #efefef; */
  /* padding: 15px; */
  position: fixed;
  bottom: 10px;
  right: 10px;
  background: #000000d1;
  color: #fff;
  display: flex;
  backdrop-filter: blur(3px);
}

.adsSpace > span{
  height: 100%;
  padding: 10px;
  width: 100%;
}

.adsDismisser{
  position: absolute;
  top: 2px;
  right: 10px;
  font-size: 20px;
}

.audio_only{
  background: #a4e8ff;
}
</style>

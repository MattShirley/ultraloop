<template>
  <div class="home">
      <!-- <b-icon-arrow-down-left-square-fill class="nav-base" v-b-hover.sidebar-right></b-icon-arrow-down-left-square-fill> -->
    <b-overlay :show="show" variant="transparent" opacity="1.0" blur="6px">
      <div class="twitch-player" height="100vh" id="twitch-embed"></div>
      <template #overlay>
        <div class="text-center">
          <b-jumbotron header="UltraLoop" lead="UltraLoop video streaming channel">
            
            <b-button
              size="sm"
              variant="primary"
              @click="triggerWatch"
            >
              Watch now!
            </b-button>
            <p><router-link to="/schedule">See full schedule</router-link></p>
          </b-jumbotron>
        </div>
      </template>
    </b-overlay>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld
  },
  data() {
    return {
      show: true,
      twitchLoaded: false
    }
  },
  mounted() {
    let twitchScript = document.createElement('script')
    twitchScript.setAttribute('src', "https://embed.twitch.tv/embed/v1.js")
    // twitchScript.async = true
    document.head.appendChild(twitchScript)

    window.addEventListener("load", function() {
      // here is the Vue code
      this.twitchEmbed = new window.Twitch.Embed("twitch-embed", {
          width: "100%",
          height: "100%",
          channel: "mst3k",
          muted: true,
          layout: "video-with-chat",
          // only needed if your site is also embedded on embed.example.com and othersite.example.com 
          // parent: ["embed.example.com", "othersite.example.com"]
        }
      )
    });
  },
  methods: {
    triggerWatch() {
      this.show = false
      this.twitchEmbed.addEventListener(window.Twitch.Embed.VIDEO_READY, () => {
          let twitchPlayer = this.twitchEmbed.getPlayer()
          twitchPlayer.setMuted(false)
        }
      )
    }
  }
}
</script>

<style scoped>
  .twitch-player {
    height: 100vh;
  }
</style>
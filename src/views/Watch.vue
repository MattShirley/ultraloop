<template>
  <div class="about">
    <!-- <vue-twitch-player
      :channel="channel"
    ></vue-twitch-player> -->
    <div id="twitch-embed"></div>
  </div>
</template>

<script>
  // import VueTwitchPlayer from 'vue-twitch-player';

  export default {
    name: 'watch',
    // ...
    components: {
      // VueTwitchPlayer,
    },
    data() {
      return {
        channel: 'ultraloop',
      };
    },
    mounted() {
      let twitchScript = document.createElement('script')
      twitchScript.setAttribute('src', "https://embed.twitch.tv/embed/v1.js")
      twitchScript.async = true
      document.head.appendChild(twitchScript)
  
      new window.Twitch.Embed("twitch-embed", {
        width: "100%",
        height: 480,
        channel: "mst3k",
        muted: false,
        layout: "video-with-chat",
        // only needed if your site is also embedded on embed.example.com and othersite.example.com 
        // parent: ["embed.example.com", "othersite.example.com"]
      });
    },
    // ...
  };
</script>
<template lang="html">

  <section class="twitch">
    <div id="twitch-embed"></div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'twitch',
    props: {
      twitchProperties: Object
    },
    mounted () {
			this.insertExternalSource();
    },
    data () {
      return {

      }
    },
    methods: {
      insertExternalSource: function(){
        var js = document.createElement("script");
        js.setAttribute("src", "https://embed.twitch.tv/embed/v1.js");
        document.getElementsByTagName("body").item(0).appendChild(js);

        var jsmain = document.createElement("script");
        jsmain.innerHTML= 'var embed = new Twitch.Embed("twitch-embed", ' + this.twitchProperties + ' );';
        document.getElementsByTagName("body").item(0).appendChild(jsmain);

        var jsmain2 = document.createElement("script");
        jsmain2.innerHTML= `
          embed.addEventListener(Twitch.Embed.VIDEO_READY, () => {
            var player = embed.getPlayer();
            player.play();
          });
        `;
        document.getElementsByTagName("body").item(0).appendChild(jsmain2);
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="scss">
  .twitch {

  }
</style>

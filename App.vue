<template>
  <div class="view" ref="viewBody">
    <transition name="hrefAnimation">
      <router-view v-show="!isAudioVisible"></router-view>
    </transition>
    <transition name="popAudio">
      <v-audio v-show="isAudioVisible"></v-audio>
    </transition>
    <v-footer></v-footer>
  </div>
</template>
<script type="text/ecmascript-6">
  import audioPlaylist from 'components/audio/AudioPlaylist';
  import footer from 'components/footer/FooterNav';
  import audio from 'components/audio/AudioView';
  import {mapMutations, mapState} from 'vuex';
  export default {
      name: 'index',
      data () {
        return {
          isAudioVisible: !1,
          musicPlayer: null
        };
      },
      components: {
          'v-footer': footer,
          'v-audio': audio,
          audioPlaylist
      },
      computed: {
        ...mapState(['isplaying'])
      },
      mounted () {
        this.musicPlayer = document.getElementById('music');
      },
      methods: {
        ...mapMutations(['play', 'pause']),
          switchPlay () {
            this.isplaying ? (this.pause(), this.musicPlayer.pause()) : (this.play(), this.musicPlayer.play());
          }
      }
  };
</script>
<style rel="stylesheet/stylus" lang="stylus">
  @import 'assets/stylus/index.styl';
  body
    background-color #1f2d3d
    .view
      position absolute
      width px2rem(750)
      height 100%
      top 0
      left 50%
      margin-left px2rem(-375)
      background url("assets/img/musicbg.jpg") no-repeat
      background-size 100% 100%
      box-shadow 0 0 px2rem(8) rgba(0,0,0,0.6)
      .mu-paper
        width 100%
        background-color transparent
        .mu-flex-row
          .flex-demo
            height px2rem(100)
            line-height px2rem(100)
            text-align center
            & i
              font-size px2rem(40)
      .mu-bottom-nav
        height px2rem(100)
        background-color transparent
        .mu-buttom-item
          min-width auto
          max-width none
          box-sizing border-box
          padding px2rem(10)
</style>

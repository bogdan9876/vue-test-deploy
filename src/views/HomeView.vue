<template>
  <div class="home">
    <h1 v-if="step === 0" class="text-big animate__animated animate__backInDown">
      Привіт
    </h1>
    <h1 v-if="step === 1" class="text-regular animate__animated animate__fadeIn">
      Сьогодні особливий день
    </h1>
    <h1 v-if="step === 2" class="text-regular animate__animated animate__pulse">
      Твій день народження 🙂
    </h1>
    <div v-if="step === 3">
      <h1  class="text-regular animate__animated animate__pulse animate__infinite">
        Головний герой це — ти, <b>Сігма</b>
      </h1>
      <div class="text-regular animate__animated animate__headShake animate__infinite">
        💪💪💪
      </div>
    </div>

    <h1 v-if="step === 4 || step === 5 || step === 6" class="text-regular animate__animated animate__bounce" style="min-height: 400px;">
      Цей подарок створений спеціально для тебе 🎁

      <div v-if="step === 5 || step === 6" class="text-small animate__animated animate__fadeIn" style="margin-top: 30px;">
        Від вершника апокаліпсису (мене).
      </div>

      <div v-if="step === 6" class="text-small animate__animated animate__fadeIn" style="margin-top: 30px;">
        Ця ідея спала на думку , після того як один дизайнер привітав відео змонтованим
      </div>
    </h1>

    <div v-if="step === 7">
      <h1 class="error" style="color: white;">
        Упс... Помилка сервера...
      </h1>
    </div>

    <h1 v-if="step === 8" class="text-regular" style="display: flex">
      <div class="animate__animated animate__swing animate__infinite">😂</div>
      А тепер без приколів
      <div class="animate__animated animate__swing animate__infinite">😂</div>
    </h1>

    <h1 v-if="step === 9" class="text-regular animate__animated animate__zoomIn">
      Давай перейдемо до головного.
      <br>
      <br>

      <AppBtn class="animate__animated animate__bounce animate__delay-1s" @click="step++">
        Починаєм
      </AppBtn>
    </h1>

    <AppWriter v-if="step === 10" @next="onWriterNext" />

    <AppAvatarScreen v-if="step === 11" />

    <audio
      :src="require('@/assets/music.mp3')"
      ref="music"
      preload
      loop
    ></audio>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import anime from 'animejs'
import 'animate.css'
import AppBtn from '@/components/AppBtn.vue'
import AppWriter from '@/components/AppWriter.vue'
import AppAvatarScreen from '@/components/AppAvatarScreen.vue'

export default defineComponent({
  name: 'HomeView',
  data (): {
    [key: string]: any
    } {
    return {
      step: 0,
      text: 'Привіт',
      interval: null
    }
  },
  components: {
    AppBtn,
    AppWriter,
    AppAvatarScreen
  },
  methods: {
    onWriterNext () {
      this.step++

      setTimeout(() => {
        (this.$refs.music as HTMLAudioElement).play()
      }, 2000)
    }
  },
  watch: {
    step (step) {
      if (step === 7) {
        clearInterval(this.interval)

        document.body.style.background = 'red'

        setTimeout(() => {
          document.querySelector('.error')!.className += ' animate__animated animate__hinge'

          setTimeout(() => {
            this.step++

            document.body.style.background = 'initial'

            setTimeout(() => this.step++, 3000)
          }, 2000)
        }, 3000)
      }
    }
  },
  mounted () {
    document.addEventListener('keydown', (e) => {
      this.step = parseInt(e.key)
      clearInterval(this.interval)
    })

    // Create a timeline with default parameters
    // const tl = anime.timeline({
    //   autoplay: true,
    //   easing: 'easeOutExpo',
    //   duration: 5750
    // })

    this.interval = setInterval(() => this.step++, 3000)

    // tl
    //   .add({
    //     targets: '.square',
    //     opacity: 1,
    //     duration: 2000,
    //     complete: () => {
    //       this.step = 1
    //     }
    //   })
    //   .add({
    //     targets: '.circle',
    //     translateX: 250
    //   })
    //   .add({
    //     targets: '.triangle',
    //     translateX: 250
    //   })
  },
  unmounted () {
    clearInterval(this.interval)
  }
})
</script>

<style lang="sass">
body
  transition: all ease

.home
  height: 100%
  display: flex
  align-items: center
  justify-content: center
  text-align: center

  .text-big
    font-size: 4rem

  .text-regular
    font-size: 2rem

  .text-small
    font-size: 1.5rem

  .center
    margin: 0 auto
</style>

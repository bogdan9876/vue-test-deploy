<template>
  <div>
    <VueWriter
      :array='arr'
      :typeSpeed="100"
      :eraseSpeed="40"
    />

    <br>
    <br>
    <AppBtn v-if="show" @click="$emit('next')">
      Далі
    </AppBtn>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// eslint-disable-next-line @typescript-eslint/ban-ts-comment
// @ts-ignore
import VueWriter from 'vue-writer'
import AppBtn from '@/components/AppBtn.vue'

export default defineComponent({
  name: 'AppWriter',
  components: {
    VueWriter,
    AppBtn
  },
  data () {
    return {
      show: false,
      arr: [
        'Надіюсь ти попав на цю сторінку і бачиш цей текст',
        'Прикольна анімація набору тексту',
        'Нехай пізнання одержимості не обійде тебе стороною',
        'як і блондинка з цінностями',
        'бажаю щоб ти навчився менеджити час ідеально',
        'щоб ти заробив для того щоб зіграти в доту',
        'щоб ти став найкращою версією себе зі всіх можливих.'
      ]
    }
  },
  mounted () {
    setTimeout(() => {
      this.show = true
    }, 40000)
  }
})
</script>

<style>
.is-typed {
  font-size: 1.5rem;
}

.is-typed span.typed {
  color: black;
}

.is-typed span.cursor {
  display: inline-block;
  width: 3px;
  background-color: black;
  animation: blink 1s infinite;
}

.is-typed span.underscore {
  display: inline-flex;
  width: 10px;
  height: 1px;
  align-items:flex-end;
  background-color: black;
  animation: blink 1s infinite;
}

.is-typed span.cursor.typing {
  animation: none;
}

@keyframes blink {
  49% {
    background-color: black;
  }
  50% {
    background-color: transparent;
  }
  99% {
    background-color: transparent;
  }
}
</style>

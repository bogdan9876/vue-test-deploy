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
        'Надіюсь ти попала на цю сторінку і бачиш цей текст',
        'Прикольна анімація набору тексту',
        'Нехай твоя майстерність і відданість справі ведуть до великих успіхів та визнання',
        'Бажаю, щоб твоя донька ніколи не дізналась , що таке сайти знайомст і подібні сервіси',
        'Лінь вбиває амбіції',
        'Страх вбиває мрії',
        'Заздрість вбиває спокій',
        'Сумнів вбиває впевненість',
        'А ТЕПЕР НАВПАКИ',
        'Амбіції вбивають лінь',
        'Мрії вбивають страх',
        'Спокій вбиває заздрість',
        'Впевненість вбиває спокій'
      ]
    }
  },
  mounted () {
    setTimeout(() => {
      this.show = true
    }, 90000)
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

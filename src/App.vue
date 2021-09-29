<template>
  <div id="app">
    <div class="bg-mainLight pt-10 pb-10">
      <div class="flex flex-col justify-center max-w-5xl w-2/3 m-auto">
        <div class="border-lightGray border-2 border-b-0 bg-white">
          <div class="-mt-0.5 border-lightGray border-t-2 p-8 bg-white"
               :class="[
                blockState_1 === 'full' && 'shadow-leftMainBlue',
                blockState_1 === 'empty' && 'shadow-leftLightGray',
                blockState_1 === 'filling' && 'shadow-leftMainGray',
                blockState_1 === 'correct' && 'shadow-leftMainGreen',
                blockState_1 === 'error' && 'shadow-leftMainPink'
                ]"
          >
            <Input class="outline-none" ref="nameInput" @input="(v) => {
              this.name = v
              checkBlock1()
            }" title="Имя"></Input>
            <Input class="mt-4 outline-none" ref="telegramInput" @input="(v) => {
              this.tg = v
              checkBlock1()
            }" title="Ник в Telegram"></Input>
            <Input class="mt-4 outline-none" ref="repoLinkInput" @input="(v) => {
              this.repoLink = v
              checkBlock1()
            }" title="Ссылка на репозиторий этого задания"></Input>
            <Input class="mt-4 outline-none" ref="dontWantToDoInput" @input="(v) => {
              this.dontWantToDo = v
              checkBlock1()
            }"
                   title="Что вы точно не хотите делать в работе, что вы делаете с неохотой?"></Input>
          </div>
          <div class="mt-2 pt-6 p-8 bg-white"
               :class="[
                blockState_2 === 'full' && 'shadow-leftMainBlue',
                blockState_2 === 'empty' && 'shadow-leftLightGray',
                blockState_2 === 'filling' && 'shadow-leftMainGray',
                blockState_2 === 'correct' && 'shadow-leftMainGreen',
                blockState_2 === 'error' && 'shadow-leftMainPink'
                ]"
          >
            <div class="mt-4 text-pt16 text-black">
              Как вы оцениваете своб способность взаимодействовать с дизайном?
            </div>
            <div class="text-pt16 mt-12 text-mainGray">
              А именно, работу с векторами, внимательность к деталям, возможность проявить инициативу - например, можете
              ли сверстать макет адаптируя его для мобильных устройств с макета под десктоп?
            </div>
            <Slider class="mt-4" @input="(v) => {
              this.designPower = v
              checkBlock2()
            }" ref="designSlider" :min=0 :value="designPower" :max=100></Slider>
            <Input class="outline-none" ref="designCommentInput" @input="(v) => this.designComment = v"
                   title="Ваш комментарий (По желанию)"></Input>
          </div>
          <div class="mt-2 pt-6 p-8 bg-white"
               :class="[
                blockState_3 === 'full' && 'shadow-leftMainBlue',
                blockState_3 === 'empty' && 'shadow-leftLightGray',
                blockState_3 === 'filling' && 'shadow-leftMainGray',
                blockState_3 === 'correct' && 'shadow-leftMainGreen',
                blockState_3 === 'error' && 'shadow-leftMainPink'
                ]"
          >
            <div class="text-pt16 text-black">
              Готовы ли работать с CSS анимацией?
            </div>
            <div class="text-pt16 mt-2 text-mainGray">
              Часто нужна несложная CSS анимация без сторонних библиотек для сопровождения какого-либо действия или
              плавной подачи информации, но без фанатизма ))
            </div>
            <Slider class="mt-4" @input="(v) => {
              this.animationsWill = v
              checkBlock3()
            }" ref="animationSlider" :min=0 :max=100 :value="animationsWill"></Slider>
            <Input class="outline-none" ref="animationCommentInput" @input="(v) => this.animationsComment = v"
                   title="Ваш комментарий (По желанию)"></Input>
          </div>
          <div class="mt-2 pt-6 p-8 bg-white"
               :class="[
                blockState_4 === 'full' && 'shadow-leftMainBlue',
                blockState_4 === 'empty' && 'shadow-leftLightGray',
                blockState_4 === 'filling' && 'shadow-leftMainGray',
                blockState_4 === 'correct' && 'shadow-leftMainGreen',
                blockState_4 === 'error' && 'shadow-leftMainPink',
                ]"
          >
            <Input class="outline-none" @input="(v) => {
              this.routines = v
              checkBlock4()
            }" ref="routineInput" title="Как относитесь к рутинной работе?"></Input>
            <div class="text-pt16 mt-2 text-mainGray">
              Бывают задачи интересные, а бывает, к примеру, нужно добавить на сайт пару новых языков в режиме
              copy/paste в файл локализации или помочь опубликовать пост в блоге - md файл из Гугл документа
            </div>
          </div>
          <div class="mt-2 pt-6 p-8 bg-white"
               :class="[
                blockState_5 === 'full' && 'shadow-leftMainBlue',
                blockState_5 === 'empty' && 'shadow-leftLightGray',
                blockState_5 === 'filling' && 'shadow-leftMainGray',
                blockState_5 === 'correct' && 'shadow-leftMainGreen',
                blockState_5 === 'error' && 'shadow-leftMainPink'
                ]"
          >
            <div class="relative h-full min-h-full bg-mainBlue w-2"></div>
            <Input class="outline-none blockElement" @input="(v) => {
              this.ifReadyForFull = v
              checkBlock5()
            }" ref="ifReadyForFullInput"
                   title="Готовы ли посвятить все 100% своего времени на работу с нашими задачами, не отвлекаясь на стороннюю разработку?"></Input>
          </div>
        </div>
        <div class="bg-white">
          <button @click="sendForm" class="h-28 text-pt20 w-full font-extralight"
                  :class="[
                buttonState === 'full' && 'shadow-mainBlueButton bg-mainBlue',
                buttonState === 'empty' && 'shadow-mainGrayButton bg-mainGray',
                buttonState === 'correct' && 'shadow-mainGreenButton bg-mainGreen',
                ]"
          >
            Отправить
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Input from '@/components/uikit/Input/Input.vue'
import Slider from "@/components/uikit/Slider/Slider"
import axios from "axios"

export default {
  name: 'App',
  components: {Input, Slider},
  data: function () {
    return {
      name: '',
      tg: '',
      repoLink: '',
      dontWantToDo: '',
      designPower: 0,
      designComment: '',
      animationsWill: 0,
      animationsComment: '',
      routines: '',
      ifReadyForFull: '',
      blockState_1: 'empty',
      blockState_2: 'empty',
      blockState_3: 'empty',
      blockState_4: 'empty',
      blockState_5: 'empty',
      buttonState: 'empty'
    }
  },
  methods: {
    checkBlock1() {
      let counter = 0
      if (this.name !== '') {
        this.$refs.nameInput.setError('')
        counter++
      }
      if (this.tg !== '') {
        this.$refs.telegramInput.setError('')
        counter++
      }
      if (this.repoLink !== '') {
        this.$refs.repoLinkInput.setError('')
        counter++
      }
      if (this.dontWantToDo !== '') {
        this.$refs.dontWantToDoInput.setError('')
        counter++
      }

      switch (counter) {
        case 0:
          this.blockState_1 = 'empty'
          break
        case 4:
          this.blockState_1 = 'full'
          break
        default:
          this.blockState_1 = 'filling'
          break
      }
      this.buttonCheck()
    },
    checkBlock2() {
      this.blockState_2 = 'full'
      this.$refs.designSlider.setError('')
      this.buttonCheck()
    },
    checkBlock3() {
      this.blockState_3 = 'full'
      this.$refs.animationSlider.setError('')
      this.buttonCheck()
    },
    checkBlock4() {
      if (this.routines !== '') {
        this.blockState_4 = 'full'
        this.$refs.routineInput.setError('')
      } else
        this.blockState_4 = 'empty'
      this.buttonCheck()
    },
    checkBlock5() {
      if (this.ifReadyForFull !== '') {
        this.blockState_5 = 'full'
        this.$refs.ifReadyForFullInput.setError('')
      } else
        this.blockState_5 = 'empty'
      this.buttonCheck()
    },
    buttonCheck() {
      if (this.blockState_1 === 'full' &&
          this.blockState_2 === 'full' &&
          this.blockState_3 === 'full' &&
          this.blockState_4 === 'full' &&
          this.blockState_5 === 'full')
        this.buttonState = 'full'
    },
    // showState: function () {
    //   console.log(`name    : ${this.name}`)
    //   console.log(`tg      : ${this.tg}`)
    //   console.log(`repo    : ${this.repoLink}`)
    //   console.log(`dontWant: ${this.dontWantToDo}`)
    //   console.log(`designPo: ${this.designPower}`)
    //   console.log(`designCo: ${this.designComment}`)
    //   console.log(`animatWi: ${this.animationsWill}`)
    //   console.log(`animatCo: ${this.animationsComment}`)
    //   console.log(`routines: ${this.routines}`)
    //   console.log(`ifReadyF: ${this.ifReadyForFull}`)
    // },
    sendForm: function () {
      let refs = this.$refs
      if (this.blockState_1 !== 'full') {
        this.blockState_1 = 'error'
        // Name field
        if (this.name === '')
          refs.nameInput.setError('Это поле необходимо заполнить')
        else
          refs.nameInput.setError('')
        // Telegram field
        if (this.tg === '')
          refs.telegramInput.setError('Это поле необходимо заполнить')
        else
          refs.telegramInput.setError('')
        // Project repository link
        if (this.repoLink === '')
          refs.repoLinkInput.setError('Это поле необходимо заполнить')
        else
          refs.repoLinkInput.setError('')
        // What you don't want to do on this work
        if (this.dontWantToDo === '')
          refs.dontWantToDoInput.setError('Это поле необходимо заполнить')
        else
          refs.dontWantToDoInput.setError('')
      }
      // Design block (only slider is checked)
      if (this.blockState_2 !== 'full') {
        refs.designSlider.setError('Необходимо указать положение')
        this.blockState_2 = 'error'
      } else {
        refs.designSlider.setError('')
      }
      // CSS Animations block (only slider is checker)
      if (this.blockState_3 !== 'full') {
        refs.animationSlider.setError('Необходимо указать положение')
        this.blockState_3 = 'error'
      } else
        refs.animationSlider.setError('')
      // Routines block (only one input checker)
      if (this.blockState_4 !== 'full') {
        refs.routineInput.setError('Это поле необходимо заполнить')
        this.blockState_4 = 'error'
      } else
        refs.routineInput.setError('')
      // Full free time on this work block (only one input checker)
      if (this.blockState_5 !== 'full') {
        refs.ifReadyForFullInput.setError('Это поле необходимо заполнить')
        this.blockState_5 = 'error'
      } else
        refs.ifReadyForFullInput.setError('')


      let val = false
      if (val) {
        axios
            .post(
                'https://script.google.com/macros/s/AKfycbwT5P8_PkFBy_vM5bhb_b-GsxQv7__15YilhVuzruB-JcFa1XXAp3kFS5_Y8a2lqg3K5A/exec',
                {
                  name: this.name,
                  telegram: this.telegram,
                  repo: this.repo,
                  sentFrom: window.location.href,
                  timestamp: Date.now(),
                  qNotWantedActivity: this.dontWantToDo,
                  qDesign: this.designPower,
                  qDesignComment: this.designComment,
                  qCssAnimation: this.animationsWill,
                  qCssAnimationComment: this.animationsComment,
                  qChores: this.routines,
                  qFreelance: this.ifReadyForFull
                },
                {
                  headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*',
                  },
                }
            )
            .then((res) => {
              console.log(res)
              if (this.blockState_1 === 'full' &&
                  this.blockState_2 === 'full' &&
                  this.blockState_3 === 'full' &&
                  this.blockState_4 === 'full' &&
                  this.blockState_5 === 'full'
              ) {
                this.blockState_1 = 'correct'
                this.blockState_2 = 'correct'
                this.blockState_3 = 'correct'
                this.blockState_4 = 'correct'
                this.blockState_5 = 'correct'

                this.buttonState = 'correct'
              }
            })
      }
    }
  },
}
</script>

<style>

#app {
  font-family: Roboto Thin, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

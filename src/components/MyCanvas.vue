<template>
  <canvas width="1280" height="720" class="canvas"></canvas>
</template>

<script>
export default {
  props: {
    background: {
      default: null
    },
    avatar: {
      default: null
    },
    avatarX: {
      default: 0
    },
    avatarY: {
      default: 0
    },
    startDay: {
      default: null
    },
    mondaySchedule: {
      default: ''
    },
    tuesdaySchedule: {
      default: ''
    },
    wednesdaySchedule: {
      default: ''
    },
    thursdaySchedule: {
      default: ''
    },
    fridaySchedule: {
      default: ''
    },
    saturdaySchedule: {
      default: ''
    },
    sundaySchedule: {
      default: ''
    }
  },
  watch: {
    background() {
      this.draw()
    },
    avatar() {
      this.draw()
    },
    avatarX() {
      this.draw()
    },
    avatarY() {
      this.draw()
    },
    startDay() {
      this.draw()
    },
    mondaySchedule() {
      this.draw()
    },
    tuesdaySchedule() {
      this.draw()
    },
    wednesdaySchedule() {
      this.draw()
    },
    thursdaySchedule() {
      this.draw()
    },
    fridaySchedule() {
      this.draw()
    },
    saturdaySchedule() {
      this.draw()
    },
    sundaySchedule() {
      this.draw()
    }
  },
  methods: {
    draw() {
      this.ctx.clearRect(0, 0, 1280, 720)
      if (this.background) {
        this.ctx.drawImage(this.background, 0, 0, 1280, 720)
      }
      if (this.avatar) {
        let scale = 1.0
        if (this.avatar.height > 720) {
          scale = 720 / this.avatar.height
        }
        const avatarSize = {
          height: this.avatar.height * scale,
          width: this.avatar.width * scale
        }
        this.ctx.drawImage(
          this.avatar,
          1280 - avatarSize.width + this.avatarX,
          this.avatarY,
          avatarSize.width,
          avatarSize.height
        )
      }
      this.ctx.drawImage(this.base, 0, 0)
      if (this.startDay && !isNaN(this.startDay)) {
        this.ctx.font = '48px serif'
        for (let i = 0; i < 7; i++) {
          const day = this.startDay + i
          this.ctx.fillText(day, 50, 120 + 85 * i)
        }
      }
      if (this.mondaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.mondaySchedule, 250, 120)
      }
      if (this.tuesdaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.tuesdaySchedule, 250, 205)
      }
      if (this.wednesdaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.wednesdaySchedule, 250, 290)
      }
      if (this.thursdaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.thursdaySchedule, 250, 375)
      }
      if (this.fridaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.fridaySchedule, 250, 460)
      }
      if (this.saturdaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.saturdaySchedule, 250, 545)
      }
      if (this.sundaySchedule) {
        this.ctx.font = '45px serif'
        this.ctx.fillText(this.sundaySchedule, 250, 630)
      }
    },
    download() {
      this.dummyLink.type = 'application/octet-stream'
      this.dummyLink.download = 'schedule.png'
      this.dummyLink.href = this.$el.toDataURL('image/png')
      this.dummyLink.click()
    }
  },
  mounted() {
    this.ctx = this.$el.getContext('2d')

    let self = this
    this.base = new Image(1280, 720)
    this.base.onload = () => {
      self.draw()
    }
    this.base.src = '/base.png'

    this.dummyLink = document.createElement('a')
  }
}
</script>

<style scoped>
.canvas {
  border: 1px solid #000;
}
</style>

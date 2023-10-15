<template>
  <div class="example">
    <MyCanvas
      :background="background"
      :avatar="avatar"
      :avatarX="avatarX"
      :avatarY="avatarY"
      :startDay="startDay"
      :mondaySchedule="mondaySchedule"
      :tuesdaySchedule="tuesdaySchedule"
      :wednesdaySchedule="wednesdaySchedule"
      :thursdaySchedule="thursdaySchedule"
      :fridaySchedule="fridaySchedule"
      :saturdaySchedule="saturdaySchedule"
      :sundaySchedule="sundaySchedule"
      ref="canvas"
    />
    <p>背景<input type="file" @change="onBackgroundChange" /></p>
    <p>アバター<input type="file" @change="onAvatarChange" /></p>
    <p v-show="avatar">
      アバターX:<input type="range" min="-500" max="500" v-model.number="avatarX" />
    </p>
    <p v-show="avatar">
      アバターY:<input type="range" min="-500" max="500" v-model.number="avatarY" />
    </p>
    <p>開始日:<input type="text" v-model.number="startDay" /></p>
    <p>月曜日の予定:<input type="text" v-model="mondaySchedule" /></p>
    <p>火曜日の予定:<input type="text" v-model="tuesdaySchedule" /></p>
    <p>水曜日の予定:<input type="text" v-model="wednesdaySchedule" /></p>
    <p>木曜日の予定:<input type="text" v-model="thursdaySchedule" /></p>
    <p>金曜日の予定:<input type="text" v-model="fridaySchedule" /></p>
    <p>土曜日の予定:<input type="text" v-model="saturdaySchedule" /></p>
    <p>日曜日の予定:<input type="text" v-model="sundaySchedule" /></p>
    <p><input type="button" value="画像ダウンロード" @click="downloadImage" /></p>
  </div>
</template>

<script>
// キャンバス用コンポーネントの読み込み
import MyCanvas from './components/MyCanvas.vue'
export default {
  components: {
    MyCanvas
  },
  methods: {
    onBackgroundChange(e) {
      const self = this
      const files = e.target.files || e.dataTransfer.files
      this.createImage(files[0], (img) => {
        self.background = img
      })
    },
    onAvatarChange(e) {
      const self = this
      const files = e.target.files || e.dataTransfer.files
      this.createImage(files[0], (img) => {
        self.avatar = img
      })
    },
    createImage(file, onloaded) {
      const reader = new FileReader()
      reader.onload = (e) => {
        var img = new Image()
        img.onload = () => {
          onloaded(img)
        }
        img.src = e.target.result
      }
      reader.readAsDataURL(file)
    },
    downloadImage() {
      this.$refs.canvas.download()
    }
  },
  data() {
    return {
      background: null,
      avatar: null,
      avatarX: 0,
      avatarY: 0,
      startDay: null,
      mondaySchedule: '',
      tuesdaySchedule: '',
      wednesdaySchedule: '',
      thursdaySchedule: '',
      fridaySchedule: '',
      saturdaySchedule: '',
      sundaySchedule: ''
    }
  }
}
</script>

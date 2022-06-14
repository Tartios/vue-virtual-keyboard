<template>
  <div>
    <KeyboardInput :areaContent="areaContent" />
    <VirtualKeyboard
    @keydown="keyEvent"
    :engKeys="engKeys"
    :ruKeys="ruKeys"
    :shiftKeyState="shiftKeyState"
    :capsKeyState="capsKeyState"
    :enLanguage="enLanguage"
    :altKeyState="altKeyState"
    />
  </div>
</template>

<script>
import VirtualKeyboard from './components/VirtualKeyboard.vue';
import KeyboardInput from './components/KeyboardInput.vue';
import { engKeys, ruKeys } from './assets/keyboard';
export default {
  name: 'App',
  components: {
    VirtualKeyboard,
    KeyboardInput,
  },
  data() {
    return {
      engKeys: engKeys,
      ruKeys: ruKeys,
      contentArray: [],
      areaContent: '',
      // служат для фиксации нажатия соответствующих клавиш и переключения языка
      shiftKeyState: false,
      capsKeyState: false,
      enLanguage: true,
      altKeyState: false,
    }
  },
  methods: {
    keyEvent(e) {
      switch(e.toLowerCase()) {
        case 'backspace':
          this.areaContent = this.areaContent.substring(0, this.areaContent.length-1);
          break;
        case 'tab':
          this.areaContent = this.areaContent + '    ';
          break;
        case 'delete':
          this.areaContent = this.areaContent.substring(0, this.areaContent.length-1);
          break;
        case 'capslock':
          this.capsKeyState = !this.capsKeyState;
          break;
        case 'enter':
          this.areaContent = this.areaContent + '\n';
          break;
        case 'shift':
          if(this.altKeyState) {
            this.enLanguage = !this.enLanguage;
            this.altKeyState = !this.altKeyState;
          } else {
            this.shiftKeyState = !this.shiftKeyState;
          }
          break;
        case 'up':
          break;
        case 'ctrl':
          break;
        case 'win':
          break;
        case 'alt':
          if(this.shiftKeyState) {
            this.enLanguage = !this.enLanguage;
            this.shiftKeyState = !this.shiftKeyState;
          } else {
            this.altKeyState = !this.altKeyState;
          }
          break;
        case 'space':
          this.areaContent = this.areaContent + ' ';
          break;
        case 'left':
          break;
        case 'down':
          break;
        case 'right':
          break;
        case 'escape':
          break;
        case 'arrowleft':
          break;
        case 'arrowright':
          break;
        case 'arrowup':
          break;
        case 'arrowdown':
          break;
        default:
          this.contentArray.push(e);
          this.areaContent = this.areaContent + e;
      }
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

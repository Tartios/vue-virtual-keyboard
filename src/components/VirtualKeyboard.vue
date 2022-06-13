<template>
    <div class="keyboard" v-show="this.enLanguage">
        <div
            class="keyboard__key"
            :class="{ double:
            key === 'Shift'
            || key === 'Backspace'
            || key === 'CapsLock'
            || key === 'Ctrl'
            || key === 'Enter'
            ? true : false,
            spaceBtn:
            key === 'Space'
            ? true : false,
            keyboard__key_active:
            (this.shiftKeyState && key.toLowerCase() === 'shift')
            || (this.capsKeyState && key.toLowerCase() === 'capslock')
            || (this.altKeyState && key.toLowerCase() === 'alt')
            ? true : false,
            active: this.keyboardKeyPush === this.key ? true : false,
            }"
            :key="key"
            @click="keyEvent"
            @keyup="keyPush"
            v-for="key in engKeys"
            >
            {{ (key === 'Shift'
            || key === 'Backspace'
            || key === 'CapsLock'
            || key === 'Ctrl'
            || key === 'Enter'
            || key === 'Tab'
            || key === 'Delete'
            || key === 'Alt'
            || key === 'Win'
            || key === 'Space'
            || key === 'Up'
            || key === 'Left'
            || key === 'Down'
            || key === 'Right')
            || this.shiftKeyState
            || this.capsKeyState
            ? key : key.toLowerCase() }}
        </div>
    </div>
    <div class="keyboard" v-show="!this.enLanguage">
        <div
            class="keyboard__key"
            :class="{ double:
            key === 'Shift'
            || key === 'Backspace'
            || key === 'CapsLock'
            || key === 'Ctrl'
            || key === 'Enter'
            ? true : false,
            spaceBtn:
            key === 'Space'
            ? true : false,
            keyboard__key_active:
            (this.shiftKeyState && key.toLowerCase() === 'shift')
            || (this.capsKeyState && key.toLowerCase() === 'capslock')
            || (this.altKeyState && key.toLowerCase() === 'alt')
            ? true : false,
            active: this.keyboardKeyPush === this.key ? true : false,
            }"
            :capsKeyState="capsKeyState"
            :key="key"
            @click="keyEvent"
            @keyup="keyPush"
            v-for="key in ruKeys"
            >
            {{ (key === 'Shift'
            || key === 'Backspace'
            || key === 'CapsLock'
            || key === 'Ctrl'
            || key === 'Enter'
            || key === 'Tab'
            || key === 'Delete'
            || key === 'Alt'
            || key === 'Win'
            || key === 'Space'
            || key === 'Up'
            || key === 'Left'
            || key === 'Down'
            || key === 'Right')
            || this.shiftKeyState
            || this.capsKeyState
            ? key : key.toLowerCase() }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            engKeys: {
                type: Object,
            },
            ruKeys: {
                type: Object,
            },
            enLanguage: {
                type: Boolean,
            },
            shiftKeyState: {
                type: Boolean,
            },
            capsKeyState: {
                type: Boolean,
            },
            altKeyState: {
                type: Boolean,
            },
            keyboardKeyPush: {
                type: String,
            },
        },
        data() {
            return {
                keys: this.enLanguage ? this.engKeys : this.ruKeys,
            }
        },
        methods: {
            keyEvent(key) {
                this.$emit('keydown', key.target.innerHTML);
            },
        },

    };
</script>

<style>
.keyboard {
    display: flex;
    flex-wrap: wrap;
    width: 1030px;
    padding: 10px;
}
.keyboard__key {
    width: 50px;
    height: 35px;
    border: 2px solid black;
    margin: 3px;
    padding: 3px;
    border-radius: 5px;
    color: white;
    font-weight: bold;
    background-color: gray;
    text-align: center;
    padding-top: 15px;
}
.keyboard__key:active {
    background-color: rgb(255, 196, 0);
}
.active {
    background-color: rgb(255, 196, 0);
}
.double {
    width: 100px;
    background-color: darkgray;
}
.spaceBtn {
    width: 265px;
}

.keyboard__key_active {
    background-color: rgb(255, 196, 0);
}
</style>
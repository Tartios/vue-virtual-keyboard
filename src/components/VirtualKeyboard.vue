<template>
    <div class="keyboard" v-show="this.enLanguage"> <!-- показывает компонент только если enLanguage true -->
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
            //фиксирует статус нажатия одной из кнопок ниже, одно нажатие - кнопка фиксируется как 'зажатая', второе - отпускает
            keyboard__key_active:(this.shiftKeyState && key.toLowerCase() === 'shift')
            || (this.capsKeyState && key.toLowerCase() === 'capslock')
            || (this.altKeyState && key.toLowerCase() === 'alt')
            ? true : false,
            active: this.keyboardKeyPush === this.key ? true : false,
            }"
            @click="keyEvent"
            v-for="key in engKeys"
            :key="key"
            >
            <!-- начальный рендер всех букв в маленьком регистре, системных кнопок - с большой буквы -->
            {{ (key === 'Shift'|| key === 'Backspace'
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
            @click="keyEvent"
            v-for="key in ruKeys"
            :key="key"
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
        },
        data() {
            return {
                keys: this.enLanguage ? this.engKeys : this.ruKeys,
                keyboardKeyPush: '',
            }
        },
        methods: {
            keyEvent(key) {
                // клик отдаст объект, нажатие клавиши - строку
                typeof(key) === 'string' ? this.$emit('keydown', key) : this.$emit('keydown', key.target.innerHTML);
            },
            keyboardEvent(e) {
            typeof(e) !== 'string' ? e = e.key : e;
            let eventKeys = document.querySelectorAll('.keyboard__key');
            let eventKey;
            // ищем на экранной клавиатуре нажатую клавишу и вешаем класс active
            eventKeys.forEach(item => {
                if(item.textContent === e) {
                    eventKey = item;
                }
            });
            eventKey.classList.add('active');
            e.toLowerCase() === 'control' ? e = 'ctrl' : e;
            this.keyboardKeyPush = e;
            this.keyEvent(e);
            this.keyboardKeyPush = '';
            setTimeout(() => {
                eventKey.classList.remove('active');
            }, 300);
            },
        },
        mounted() {
            document.addEventListener('keyup', this.keyboardEvent)
        }
    };
</script>

<style>
.keyboard {
    display: flex;
    flex-wrap: wrap;
    margin: 0 auto;
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
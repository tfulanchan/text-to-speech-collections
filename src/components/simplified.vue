<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'simplified',
    setup() {
        let synth = speechSynthesis;
        const voices = speechSynthesis.getVoices();
        const submit = (event) => {
            event.preventDefault();
            const utterThis = new SpeechSynthesisUtterance(message.value);
            // utterThis.lang = 'zh-CN';
            const voices = window.speechSynthesis.getVoices();
            // utterThis.voice = voices.find(voice => voice.name === `${selected.selectedOptions[0].textContent}`);
            let selectedOption = selected.selectedOptions[0];
            let attributeValue = selectedOption.getAttribute("data-lang");
            utterThis.voice = voices.find(voice => voice.lang === `${attributeValue}`);
            // utterThis.voice = 'Google 普通话（中国大陆）';
            utterThis.pitch = 1;
            // console.log(voices, 'getVoices()')
            // console.log(selectedOption, ' selectedOption ')
            console.log(attributeValue, ' selected.selectedOptions[0] ');
            // console.log(utterThis, 'utterThis')
            // console.log(message._value.length, '      message._value.length a')
            synth.speak(utterThis);
        };
        const pause = (event) => {
            window.speechSynthesis.pause();
            // const char = event.utterThis.text.charAt(event.charIndex);
            // console.log(
            //     `Speech paused at character ${event.charIndex} of "${event.utterance.text}", which is "${char}".`,
            // );
        }

        const cancel = () => {
            window.speechSynthesis.cancel();
        }

        const resume = () => {
            window.speechSynthesis.resume();
        }
        const message = ref('')

        const list = ref([1, 2, 3])
        const itemRefs = ref([])
        return {
            message,
            submit,
            synth,
            voices,
            pause,
            cancel,
            resume,
        }
    }
})

</script>

<template>
    <body>
        <div class="wrapper">
            <header>Text To Speech</header>
            <form id="myForm" action="#">
                <div class="row">
                    <p>Message is: {{ message }}</p>
                    <textarea v-model="message"></textarea>
                </div>
                <div class="row">
                    <label>Select Voice</label>
                    <div class="outer">
                        <select id="selected">
                            <option data-lang="zh-CN">Google 普通话（中国大陆）</option>
                            <option data-lang="zh-HK">Google 粤語（香港）</option>
                            <option data-lang="zh-TW">Google 國語（臺灣）</option>
                        </select>
                    </div>
                </div>
                <button @click="submit">listen</button>
                <button @click="pause">pause</button>
                <button @click="resume">resume</button>
                <button @click="cancel">cancel</button>
            </form>
        </div>
    </body>
</template>

<style scoped>
/* Import Google Font - Poppins */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    background: #0a52a4;
}

::selection {
    color: #fff;
    background: #5256AD;
}

.wrapper {
    width: 370px;
    padding: 25px 30px;
    border-radius: 7px;
    background: #fff;
    box-shadow: 7px 7px 20px rgba(0, 0, 0, 0.05);
}

.wrapper header {
    font-size: 28px;
    font-weight: 500;
    text-align: center;
}

.wrapper form {
    margin: 35px 0 20px;
}

form .row {
    display: flex;
    margin-bottom: 20px;
    flex-direction: column;
}

form .row label {
    font-size: 18px;
    margin-bottom: 5px;
}

form .row:nth-child(2) label {
    font-size: 17px;
}

/* , button */
form :where(textarea, select) {
    outline: none;
    width: 100%;
    height: 100%;
    border: none;
    border-radius: 5px;
}

form .row textarea {
    resize: none;
    height: 110px;
    font-size: 15px;
    padding: 8px 10px;
    border: 1px solid #999;
}

form .row textarea::-webkit-scrollbar {
    width: 0px;
}

form .row .outer {
    height: 47px;
    display: flex;
    padding: 0 10px;
    align-items: center;
    border-radius: 5px;
    justify-content: center;
    border: 1px solid #999;
}

form .row select {
    text-align: center;
    font-size: 14px;
    background: none;
}

form .row select::-webkit-scrollbar {
    width: 8px;
}

form .row select::-webkit-scrollbar-track {
    background: #fff;
}

form .row select::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 8px;
    border-right: 2px solid #ffffff;
}

form button {
    height: 52px;
    width: 25%;
    color: #fff;
    font-size: 17px;
    cursor: pointer;
    margin-top: 10px;
    background: #4b2e83;
    transition: 0.3s ease;
    cursor: pointer;
    outline: none;
    border: solid 1px rgba(255, 255, 255, 1);
}

form button:hover {
    background: #636363;
}

@media(max-width: 400px) {
    .wrapper {
        max-width: 345px;
        width: 100%;
    }
}
</style>

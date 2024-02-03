<template>
    <div class="wrapper">
        <header>Text To Speech</header>
        <form action="#">
            <div class="row">
                <label>Enter Text</label>
                <textarea v-model="message"></textarea>
            </div>
            <div class="row">
                <label>Select Voice</label>
                <div class="outer">
                    <select ref="voiceSelect"></select>
                </div>
            </div>
            <button @click="toggleSpeech">{{ isSpeaking ? 'Pause Speech' : 'Convert To Speech' }}</button>
        </form>
    </div>
</template>
  
<script>
import { defineComponent, ref, onMounted, watch } from 'vue';
import { useSpeechSynthesis } from '@vueuse/core';

export default defineComponent({
    setup() {
        const { isSupported, speak, stop, utterance } = useSpeechSynthesis();
        const message = ref('');
        const voiceSelect = ref(null);
        const isSpeaking = ref(false);

        onMounted(() => {
            console.log(useSpeechSynthesis(), ' useSpeechSynthesis() ')
            if (isSupported.value) {
                // Populate the voice list
                const voices = utterance.value;
                voiceSelect.value.innerHTML = '';
                for (let voice of voices) {
                    let selected = voice.name === "Google US English" ? "selected" : "";
                    let option = `<option value="${voice.name}" ${selected}>${voice.name} (${voice.lang})</option>`;
                    voiceSelect.value.insertAdjacentHTML("beforeend", option);
                }
            }
        });

        const toggleSpeech = () => {
            if (isSpeaking.value) {
                stop();
                isSpeaking.value = false;
            } else {
                speak(message.value);
                isSpeaking.value = true;
            }
        };

        watch(message, () => {
            if (isSpeaking.value) {
                stop();
                speak(message.value);
            }
        });

        return {
            message,
            voiceSelect,
            isSpeaking,
            toggleSpeech
        };
    }
});
</script>
  
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

form :where(textarea, select, button) {
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
    color: #fff;
    font-size: 17px;
    cursor: pointer;
    margin-top: 10px;
    background: #675AFE;
    transition: 0.3s ease;
}

form button:hover {
    background: #4534fe;
}

@media(max-width: 400px) {
    .wrapper {
        max-width: 345px;
        width: 100%;
    }
}
</style>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    setup() {
        const splitText = (text, from, to) => [
            text.slice(0, from),
            text.slice(from, to),
            text.slice(to)
        ];
        const HighlightedText = ({ text, from, to }) => {
            const [start, highlight, finish] = splitText(text, from, to);
            return (
                `${start}<span style="background-color:yellow;">${highlight}</span>${finish}`
            );
        };

        const highlight = (text, from, to) => {
            let replacement = highlightBackground(text.slice(from, to));
            return text.substring(0, from) + replacement + text.substring(to);
        };
        const highlightBackground = (sample) =>
            `<span style="background-color:yellow;">${sample}</span>`;
        const message = ref('ACTION REQUIRED! To complete the sign up process, simply click the link in the email or copy it into your web browser.')
        const read = () => {
            const synth = window.speechSynthesis;
            if (!synth) {
                console.error("no tts");
                return;
            }
            let text = document.getElementById("text");
            let originalText = text.innerText;
            let utterance = new SpeechSynthesisUtterance(originalText);
            utterance.addEventListener("boundary", (event) => {
                const { charIndex, charLength } = event;
                text.innerHTML = highlight(
                    originalText,
                    charIndex,
                    charIndex + charLength
                );
            });
            // utterance.lang = 'zh-HK'

            // synth.speak(utterance);
        }
        return {
            splitText,
            highlightBackground,
            read,
            message,
            HighlightedText,
            highlight,
        }
    }
})
</script>
<template>
    <div id="text">
        {{ message }}
    </div>
    <button id="btn" @click="read">klik me</button>
</template>
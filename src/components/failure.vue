<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'failure',
  setup() {
    let synth = speechSynthesis;
    const voices = speechSynthesis.getVoices();
    const content = ref('The charIndex read-only property of the SpeechSynthesisUtterance interface returns the index position of the character in SpeechSynthesisUtterance.text that was being spoken when the event was triggered.')
    const utterThis = new SpeechSynthesisUtterance(content.value);
    // const pause = (event) => {
    //   const char = event.utterThis.text.charAt(event.charIndex);
    //   console.log(
    //     `Speech paused at character ${event.charIndex} of "${event.utterThis.text}", which is "${char}".`,
    //   );
    // };
    // const read = (event) => {
    //   event.preventDefault();
    //   const utterThis = new SpeechSynthesisUtterance(content.value);
    //   utterThis.pitch = 1;
    //   synth.speak(utterThis);
    // }
    const bound = () => {
 
    }
    return {
      synth,
      voices,
      content,
      // read,
      // pause
      bound,
      utterThis
    }
  }
})

</script>
<template>
  <div class="wrapper">
    <p>{{ content }}</p>
    <button @click="bound">hello</button>
    <button @click="pause">pause</button>
  </div>
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
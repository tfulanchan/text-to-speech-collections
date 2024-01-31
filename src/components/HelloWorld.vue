<script setup>
import { ref } from 'vue'
const message = ref('')

function populateVoiceList() {
  if (typeof speechSynthesis === "undefined") {
    return;
  }

  const voices = speechSynthesis.getVoices();

  for (let i = 0; i < voices.length; i++) {
    const option = document.createElement("option");
    option.textContent = `${voices[i].name} (${voices[i].lang})`;

    if (voices[i].default) {
      option.textContent += " — DEFAULT";
    }

    option.setAttribute("data-lang", voices[i].lang);
    option.setAttribute("data-name", voices[i].name);
    document.getElementById("voiceSelect").appendChild(option);
  }
}

populateVoiceList();
if (
  typeof speechSynthesis !== "undefined" &&
  speechSynthesis.onvoiceschanged !== undefined
) {
  speechSynthesis.onvoiceschanged = populateVoiceList;
}
// inputForm.onsubmit = (event) => {
//   event.preventDefault();

//   const utterThis = new SpeechSynthesisUtterance(inputTxt.value);
//   const selectedOption =
//     voiceSelect.selectedOptions[0].getAttribute("data-name");
//   for (let i = 0; i < voices.length; i++) {
//     if (voices[i].name === selectedOption) {
//       utterThis.voice = voices[i];
//     }
//   }
//   synth.speak(utterThis);
//   inputTxt.blur();
// };
const form = document.getElementById("myForm");

console.log(speechSynthesis)
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
          <select id="voiceSelect"></select>
        </div>
      </div>
      <input type="submit" value="Submit">
      <button type="submit" value="Submit">Convert To Speech</button>
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
  background: #5256AD;
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

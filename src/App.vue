<template>
  <div id="app">
    <div id="left">
      <input type="text" class="input" placeholder="PALAVRA" />
      <input type="text" class="input" id="tipInput" placeholder="DICA" />

      <ButtonPlay @onClick="play" />

      <p id="choseWord">{{ choseWord }}</p>

      <span>
        <Button id="A" label="A" @onClick="letterPlay"></Button>
        <Button id="B" label="B" @onClick="letterPlay"></Button>
        <Button id="C" label="C" @onClick="letterPlay"></Button>
        <Button id="D" label="D" @onClick="letterPlay"></Button>
        <Button id="E" label="E" @onClick="letterPlay"></Button>
        <Button id="F" label="F" @onClick="letterPlay"></Button>
      </span>
      <span>
        <Button id="G" label="G" @onClick="letterPlay"></Button>
        <Button id="H" label="H" @onClick="letterPlay"></Button>
        <Button id="I" label="I" @onClick="letterPlay"></Button>
        <Button id="J" label="J" @onClick="letterPlay"></Button>
        <Button id="K" label="K" @onClick="letterPlay"></Button>
        <Button id="L" label="L" @onClick="letterPlay"></Button>
      </span>
      <span>
        <Button id="M" label="M" @onClick="letterPlay"></Button>
        <Button id="N" label="N" @onClick="letterPlay"></Button>
        <Button id="O" label="O" @onClick="letterPlay"></Button>
        <Button id="P" label="P" @onClick="letterPlay"></Button>
        <Button id="Q" label="Q" @onClick="letterPlay"></Button>
        <Button id="R" label="R" @onClick="letterPlay"></Button>
      </span>
      <span>
        <Button id="S" label="S" @onClick="letterPlay"></Button>
        <Button id="T" label="T" @onClick="letterPlay"></Button>
        <Button id="U" label="U" @onClick="letterPlay"></Button>
        <Button id="V" label="V" @onClick="letterPlay"></Button>
        <Button id="X" label="X" @onClick="letterPlay"></Button>
        <Button id="W" label="W" @onClick="letterPlay"></Button>
      </span>
      <span>
        <Button id="Y" label="Y" @onClick="letterPlay"></Button>
        <Button id="Z" label="Z" @onClick="letterPlay"></Button>
      </span>

      <ButtonNewPlay @onClick="newPlay" />
    </div>

    <div id="right">
      <p id="separateLetters">{{ name }}</p>
      <p id="result">{{ result }}</p>
      <img :src="image" id="image" />
      <audio id="hitSound" src="./assets/sounds/acertou.mp3"></audio>
      <audio id="errorSound" src="./assets/sounds/errou.mp3"></audio>
      <audio id="victorySound" src="./assets/sounds/vitoria.mp3"></audio>
      <audio id="defeatSound" src="./assets/sounds/derrota.mp3"></audio>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button";
import ButtonPlay from "./components/ButtonPlay";
import ButtonNewPlay from "./components/ButtonNewPlay";

import Hangman from './assets/imgs/hangman.png';
import Head from "./assets/imgs/head.png";
import Body from "./assets/imgs/body.png";
import LeftArm from "./assets/imgs/leftArm.png";
import RightArm from "./assets/imgs/rightArm.png";
import RightLeg from "./assets/imgs/rightLeg.png";
import LeftLeg from "./assets/imgs/leftLeg.png";
import Defeat from "./assets/imgs/defeat.png";
import Victory from "./assets/imgs/victory.png";

export default {
  components: { Button, ButtonPlay, ButtonNewPlay },

  data: function() {
    return {
      hits: 0,
      name: [],
      choseWord: "",
      result: "",
      counter: 0,
      image: Hangman,
      tips: "",
      word: ""
    };
  },
  methods: {
    letterPlay(n) {
      let index = this.choseWord.indexOf(n);

      if (index === -1) {
        this.counter++;
        document.querySelector("#" + n).style.backgroundColor = "rgb(255, 24, 50)"
        document.querySelector("#" + n).style.color = "#fff"
        document.querySelector("#" + n).disabled = true
        document.querySelector("#errorSound").play()
      } else {
        while (index != -1) {
          this.name.splice(index, 1, n);
          document.querySelector("#hitSound").play();
          document.querySelector("#" + n).style.backgroundColor = "rgb(97, 97, 247)"
          document.querySelector("#" + n).style.color = "#fff"
          document.querySelector("#" + n).disabled = true
          this.hits++;
          this.checkWord();
          index = this.choseWord.indexOf(n, index + 1);
        }
      }

      if (this.counter !== 0) {
        this.changeImage();
      }
      if (this.hits == 3) {
        this.result = `A dica é: ${this.tips}`;
      }

      
    },
    checkWord() {
      let finalWord = this.choseWord.join(",");
      let finalName = this.name.join(",");
      if (finalName == finalWord) {
        document.querySelector("#right").style.backgroundColor = "rgb(97, 97, 247)";
        this.image = Victory;
        document.querySelector("#hitSound").pause();
        document.querySelector("#victorySound").play();
        this.name = `A palavra é ${this.choseWord.join("")}`
        this.result = "Parabéns, você acertou!!";
      }
    },
    play() {
      this.word = document.querySelector(".input").value.split("");
      document.querySelector(".input").value = "";

      this.tips = document.querySelector("#tipInput").value
      document.querySelector("#tipInput").value = "";

      document.querySelector("#choseWord").innerHTML = `A palavra tem ${this.word.length} letras`;

      this.choseWord = this.word;
      for (let i in this.choseWord) {
        let change = this.choseWord[i].replace(this.choseWord[i], "__");
        this.name.push(change);
      }
      
    },
    newPlay() {

      document.location.reload(true);

    },
    changeImage() {
      if (this.counter == 1) {
        this.image = Head;
      }
      if (this.counter == 2) {
        this.image = Body;
      }
      if (this.counter == 3) {
        this.image = LeftLeg;
      }
      if (this.counter == 4) {
        this.image = RightLeg;
      }
      if (this.counter == 5) {
        this.image = LeftArm;
      }
      if (this.counter == 6) {
        this.image = RightArm;
      }
      if (this.counter == 7) {
        this.image = Defeat;
        document.querySelector("#right").style.backgroundColor = "rgb(255, 24, 50)";
        this.result = "Você perdeu! Tente novamente.";
        document.querySelector("#errorSound").pause()
        document.querySelector("#defeatSound").play();
        this.name = `A palavra é ${this.choseWord.join("")}`
      }
    }
  }
};
</script>

<style>
body {
  background: rgb(177, 118, 96);
}

#app {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

#left {
  display: flex;
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#right {
  display: flex;
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(185, 167, 167);
}

#app span {
  margin: 5px;
  margin-right: 5px;
}

#choseWord {
  font-size: 1.5rem;
}

.input {
  height: 30px;
  width: 300px;
  margin-bottom: 10px;
}

#result {
  font-size: 2.5rem;
  color: #fff;
  text-align: center;
}

#separateLetters {
  text-align: center;
  font-size: 2.5rem;
}
</style>
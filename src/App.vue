<template>
  <div id="app">
    <div id="esquerdo">
      <input type="text" class="input" placeholder="PALAVRA" />
      <input type="text" class="input" id="dicaInput" placeholder="DICA" />

      <ButtonPlay @onClick="play" />

      <p id="palavra">{{ palavra }}</p>

      <span>
        <Button label="A" @onClick="letra"></Button>
        <Button label="B" @onClick="letra"></Button>
        <Button label="C" @onClick="letra"></Button>
        <Button label="D" @onClick="letra"></Button>
        <Button label="E" @onClick="letra"></Button>
        <Button label="F" @onClick="letra"></Button>
      </span>
      <span>
        <Button label="G" @onClick="letra"></Button>
        <Button label="H" @onClick="letra"></Button>
        <Button label="I" @onClick="letra"></Button>
        <Button label="J" @onClick="letra"></Button>
        <Button label="K" @onClick="letra"></Button>
        <Button label="L" @onClick="letra"></Button>
      </span>
      <span>
        <Button label="M" @onClick="letra"></Button>
        <Button label="N" @onClick="letra"></Button>
        <Button label="O" @onClick="letra"></Button>
        <Button label="P" @onClick="letra"></Button>
        <Button label="Q" @onClick="letra"></Button>
        <Button label="R" @onClick="letra"></Button>
      </span>
      <span>
        <Button label="S" @onClick="letra"></Button>
        <Button label="T" @onClick="letra"></Button>
        <Button label="U" @onClick="letra"></Button>
        <Button label="V" @onClick="letra"></Button>
        <Button label="X" @onClick="letra"></Button>
        <Button label="W" @onClick="letra"></Button>
      </span>
      <span>
        <Button label="Y" @onClick="letra"></Button>
        <Button label="Z" @onClick="letra"></Button>
      </span>

      <ButtonNewPlay @onClick="newPlay" />
    </div>

    <div id="direito">
      <p id="montagem">{{ nome }}</p>
      <p id="resultado">{{ result }}</p>
      <img :src="imagem" id="imagem" />
      <audio id="soundAcerto" src="./assets/sounds/acertou.mp3"></audio>
      <audio id="soundErro" src="./assets/sounds/errou.mp3"></audio>
      <audio id="soundVitoria" src="./assets/sounds/vitoria.mp3"></audio>
      <audio id="soundDerrota" src="./assets/sounds/derrota.mp3"></audio>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button";
import ButtonPlay from "./components/ButtonPlay";
import ButtonNewPlay from "./components/ButtonNewPlay";
import Cabeca from "./assets/imgs/cabeca.png";
import Tronco from "./assets/imgs/tronco.png";
import BracoE from "./assets/imgs/bracoE.png";
import BracoD from "./assets/imgs/bracoD.png";
import PernaD from "./assets/imgs/pernaD.png";
import PernaE from "./assets/imgs/pernaE.png";
import Lose from "./assets/imgs/rosto.png";
import Win from "./assets/imgs/win.png";

export default {
  components: { Button, ButtonPlay, ButtonNewPlay },

  data: function() {
    return {
      acertos: 0,
      nome: [],
      palavra: "",
      result: "",
      contador: 0,
      imagem: "",
      dicas: ""
    };
  },
  methods: {
    letra(n) {
      let indice = this.palavra.indexOf(n);

      if (indice === -1) {
        this.contador++;
        document.querySelector("#soundErro").play();
      } else {
        while (indice != -1) {
          this.nome.splice(indice, 1, n);
          document.querySelector("#soundAcerto").play();
          this.acertos++;
          this.verificar();
          indice = this.palavra.indexOf(n, indice + 1);
        }
      }

      if (this.contador !== 0) {
        this.changeImage();
      }
      if (this.acertos == 3) {
        this.result = this.dicas;
      }
    },
    verificar() {
      let palavra = this.palavra.join(",");
      let nome = this.nome.join(",");
      if (nome == palavra) {
        document.querySelector("#direito").style.backgroundColor =
          "rgb(97, 97, 247)";
        this.result = "Parabéns, você acertou!!";
        document.querySelector("#soundVitoria").play();
        this.contador = 0;
        this.imagem = Win;
      }
    },
    play() {
      var word = document.querySelector(".input").value.split("");
      document.querySelector(".input").value = "";
      document.querySelector(
        "#palavra"
      ).innerHTML = `A palavra tem ${word.length} letras`;
      this.palavra = word;
      for (let i in this.palavra) {
        let troca = this.palavra[i].replace(this.palavra[i], "__");
        this.nome.push(troca);
      }
      this.dicas = document.querySelector("#dicaInput").value;
      document.querySelector("#dicaInput").value = "";
    },
    newPlay() {
      this.nome = [];
      this.palavra = "";
      this.result = "";
      this.contador = 0;
      this.acertos = 0;
      this.imagem = "";
      document.querySelector("#palavra").innerHTML = "";
      document.querySelector("#direito").style.backgroundColor =
        "rgb(185, 167, 167)";
      document.querySelector("#soundVitoria").pause();
      document.querySelector("#soundDerrota").pause();
    },
    changeImage() {
      if (this.contador == 1) {
        this.imagem = Cabeca;
      }
      if (this.contador == 2) {
        this.imagem = Tronco;
      }
      if (this.contador == 3) {
        this.imagem = PernaE;
      }
      if (this.contador == 4) {
        this.imagem = PernaD;
      }
      if (this.contador == 5) {
        this.imagem = BracoE;
      }
      if (this.contador == 6) {
        this.imagem = BracoD;
      }
      if (this.contador == 7) {
        this.imagem = Lose;
        document.querySelector("#direito").style.backgroundColor =
          "rgb(255, 24, 50)";
        this.result = "Você perdeu! Tente novamente.";
        document.querySelector("#soundDerrota").play();
        this.nome = this.palavra;
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

#esquerdo {
  display: flex;
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#direito {
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

#palavra {
  font-size: 1.5rem;
}

.input {
  height: 30px;
  width: 300px;
  margin-bottom: 10px;
}

#resultado {
  font-size: 1.5rem;
  color: #fff;
  text-align: center;
}

#montagem {
  text-align: center;
  font-size: 1.5rem;
}
</style>
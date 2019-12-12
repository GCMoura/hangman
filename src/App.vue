<template>
    <div id="app">
        <div id="esquerdo">

            <input type="text" class="input" >
            <button class="buttonPlay" @click="play"> Jogar </button>
            
            <p id="palavra"> {{ palavra }} </p>
           
        <br>
        <span>
        <Button label="A" @onClick="letra"></Button>
        <Button label="B" @onClick="letra"></Button>
        <Button label="C" @onClick="letra"></Button>
        <Button label="D" @onClick="letra"></Button>
        <Button label="E" @onClick="letra"></Button>
        <Button label="F" @onClick="letra"></Button>
        </span> <span>
        <Button label="G" @onClick="letra"></Button>
        <Button label="H" @onClick="letra"></Button>
        <Button label="I" @onClick="letra"></Button>
        <Button label="J" @onClick="letra"></Button>
        <Button label="K" @onClick="letra"></Button>
        <Button label="L" @onClick="letra"></Button>
        </span> <span>
        <Button label="M" @onClick="letra"></Button>
        <Button label="N" @onClick="letra"></Button>
        <Button label="O" @onClick="letra"></Button>
        <Button label="P" @onClick="letra"></Button>
        <Button label="Q" @onClick="letra"></Button>
        <Button label="R" @onClick="letra"></Button>
        </span> <span>
        <Button label="S" @onClick="letra"></Button>
        <Button label="T" @onClick="letra"></Button>
        <Button label="U" @onClick="letra"></Button>
        <Button label="V" @onClick="letra"></Button>
        <Button label="X" @onClick="letra"></Button>
        <Button label="W" @onClick="letra"></Button>
        </span> <span>
        <Button label="Y" @onClick="letra"></Button>
        <Button label="Z" @onClick="letra"></Button>
        </span>
        
        <p>{{ nome }}</p>


        <button class="buttonNewPlay" @click="newPlay"> Novo jogo </button>
        </div>

        <div id="direito">
            Oi
            <p id="resultado" > {{ result }} </p>
            <div id="imagem"> {{imagem}} </div>
            
        </div>
        
  </div>
</template>

<script>
import Button from './components/Button'

export default {
    components: { Button },

    data: function(){
        return {
            nome: [],
            palavra: '',
            result: '',
            contador: 0,
            imagem: './static/tronco.jpg'
        }
    },
    methods: {
        letra(n) {
            
            if (n === this.palavra) {
                var indice = this.palavra.indexOf(n)
                this.nome.splice(indice, 0, n)
            } 
            if (n !== this.palavra){
                this.contador++
                console.log('Contador ' + this.contador)
            }             

            if (this.contador != 0) {
                this.changeImage()
            }

            if (this.nome.length === this.palavra.length){
                document.querySelector('#direito').style.backgroundColor = 'rgb(97, 97, 247)'
                this.result = "Parabéns, você acertou!!"
            }
        },
        play() {
            var word = document.querySelector('.input').value         
            document.querySelector('.input').value = ""
            this.palavra = word
        },
        newPlay() {
            this.nome = []
            this.palavra = ''
            this.result = ''
            this.contador = 0
            document.querySelector('#direito').style.backgroundColor = 'rgb(185, 167, 167)'
        },
        changeImage() {
            if (this.contador == 1) {
                console.log('trocar imagem')
                this.imagem = './assets/3.png'
            }
        }
    }
}
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

.buttonPlay {
    height: 35px;
    width: 80px;
    background-color: rgb(185, 167, 167);
    font-size: 1.2rem;
    margin-left: 10px;
}

.buttonNewPlay {
    height: 35px;
    width: 200px;
    background-color: rgb(185, 167, 167);
    font-size: 1.2rem;
    margin-left: 10px;
}

#resultado {
    font-size: 1.5rem;
    color: #fff;  
    text-align: center;
}



</style>
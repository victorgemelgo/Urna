<template>
  <section class="d-flex justify-content-center align-items-center" style="margin-top: 100px">
    <div id="urna" class="d-flex justify-content-around align-items-center">
      <div id="display" class="text-black d-flex justify-content-lg-between p-3">
        <div>
          <h3 class="mt-5">{{ nome }}</h3>
          <div class="mt-5">
            <div class="">
              <label>Numero: </label>
              <input type="number" readonly maxlength="5" v-model="numero" />
            </div>

            <div>
              <label>Partido: </label>
              <span style="margin-left: 15px">{{ partido }}</span>
              <p>{{ validaVoto }}</p>
            </div>
          </div>
        </div>
        <div id="foto">
          <img src="" alt="" />
        </div>
      </div>
      <div id="buttons bg-warning">
        <div class="d-flex btn-numeros">
          <button class="btn" @click="addNumber(1)">1</button>
          <button class="btn" @click="addNumber(2)">2</button>
          <button class="btn" @click="addNumber(3)">3</button>
        </div>
        <div class="d-flex btn-numeros">
          <button class="btn" @click="addNumber(4)">4</button>
          <button class="btn" @click="addNumber(5)">5</button>
          <button class="btn" @click="addNumber(6)">6</button>
        </div>
        <div class="d-flex btn-numeros">
          <button class="btn" @click="addNumber(7)">7</button>
          <button class="btn" @click="addNumber(8)">8</button>
          <button class="btn" @click="addNumber(9)">9</button>
        </div>
        <div class="d-flex btn-numeros justify-content-center">
          <button class="btn" @click="addNumber(0)">0</button>
        </div>
        <div class="d-flex btn-numeros justify-content-center">
          <button class="btn border bg-white text-black" @click="branco">Branco</button>
          <button class="btn btn-warning text-black" @click="corrige">Corrige</button>
          <button class="btn btn-success text-black" @click="confirma">Confirma</button>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#urna {
  height: 400px;
  width: 800px;
  background-color: rgb(213, 213, 213);
  color: black;
}

#display {
  background-color: white;
  width: 60%;
  height: 300px;
  border-radius: 10px;
  border: 5px solid black;
}

#foto {
  width: 150px;
  height: 150px;
  background-color: rgb(213, 213, 213);
  border-radius: 10px;
  border: 3px solid black;
  margin-top: 20%;
}

.btn-numeros button {
  color: black;
  width: 80px;
  height: 60px;
  margin: 5px;
}

input {
  border: 0.5px solid grey;
  width: 100px;
  margin-left: 10px;
}

input:focus {
  outline: none;
}
</style>

<script setup>
import { ref } from 'vue'

const numero = ref('')
const nome = ref('Nome do Candidato')
const partido = ref('')
const validaVoto = ref(false)

const listaCandidatos = [
  {
    numero: 101234,
    nome: 'João da Silva',
    partido: 'Partido dos trabalhadores',
    foto: 'src/assets/images/foto.jpg'
  },
  {
    numero: 111234,
    nome: 'Maria de Souza',
    partido: 'Partido da união',
    foto: 'src/assets/images/foto.jpg'
  },
  {
    numero: 121234,
    nome: 'Wesley Santos',
    partido: 'Partido Democratico',
    foto: 'src/assets/images/foto.jpg'
  }
]

const audioBtn = new Audio('src/assets/sounds/btn-sound.mp3')
const audioConfirm = new Audio('src/assets/sounds/btn-conf-sound.mp3')

function addNumber(n) {
  numero.value += n
  audioBtn.play()

  if (numero.value.length > 6) {
    numero.value = numero.value.slice(0, 6)
  }

  if (numero.value.length === 6) {
    const candidato = listaCandidatos.find((c) => c.numero === parseInt(numero.value))
    if (candidato) {
      nome.value = candidato.nome
      partido.value = candidato.partido
      validaVoto.value = true
    } else {
      nome.value = 'Candidato não encontrado'
      partido.value = ''
      validaVoto.value = false
    }
  } else {
    nome.value = 'Nome do Candidato'
    partido.value = ''
  }
}

function corrige() {
  numero.value = ''
  nome.value = 'Nome do Candidato'
  partido.value = ''
  validaVoto.value = false 
  audioBtn.play()
}

function branco() {
  numero.value = '000000'
  nome.value = 'Voto em Branco'
  audioBtn.play()
}

function confirma() {
  if (validaVoto.value == true) {
    audioConfirm.play()
  }
}
</script>

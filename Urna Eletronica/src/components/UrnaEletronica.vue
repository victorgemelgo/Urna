<template>
  <section class="d-flex justify-content-center align-items-center" style="margin-top: 100px">
    <div id="urna" class="d-flex justify-content-around align-items-center">
      <div id="display" class="text-black d-flex">
        <div>
          <h3 class="align-self-start">Nome Candidato</h3>
          <div class="align-self-end bg-secondary">
            <div class="">
              <label>Numero: </label>
              <input type="number" readonly v-model="inputNumero" />
            </div>

            <div>
              <label>Nome: </label>
              <span>asdasd</span>
            </div>

            <div>
              <label>Partido: </label>
              <span>{{ inputNumero }}</span>
            </div>
          </div>
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
          <button class="btn border bg-white text-black" @click="">Branco</button>
          <button class="btn btn-warning text-black" @click="corrige">Corrige</button>
          <button class="btn btn-success text-black" @click="">Confirma</button>
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
  width: 50%;
  height: 300px;
  border-radius: 10px;
  border: 8px solid black;
}

.btn-numeros button {
  color: black;
  width: 80px;
  height: 60px;
  margin: 5px;
}
</style>

<script setup>
import { ref } from 'vue'

const inputNumero = ref('')

function addNumber(n) {
  inputNumero.value += n
}

function corrige() {
    inputNumero.value = ''
}
</script>

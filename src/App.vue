<script setup>
import { ref } from 'vue'

const title = ref("Seu perfil");
const user = ref({
  nome: '',
  sobrenome: '',
  data: '',
  email: '',
  senha: '',
  senhaconfirm: '',
  cidade: '',
  estado: '',
  rua: '',
  bairro:'',
  hobbies: [],
  linguagempref: ''
})

const estados = [
  { uf: 'AC', name: 'Acre' },
  { uf: 'AL', name: 'Alagoas' },
  { uf: 'AP', name: 'Amapá' },
  { uf: 'AM', name: 'Amazonas' },
  { uf: 'BA', name: 'Bahia' },
  { uf: 'CE', name: 'Ceará' },
  { uf: 'DF', name: 'Distrito Federal' },
  { uf: 'ES', name: 'Espírito Santo' },
  { uf: 'GO', name: 'Goiás' },
  { uf: 'MA', name: 'Maranhão' },
  { uf: 'MT', name: 'Mato Grosso' },
  { uf: 'MS', name: 'Mato Grosso do Sul' },
  { uf: 'MG', name: 'Minas Gerais' },
  { uf: 'PA', name: 'Pará' },
  { uf: 'PB', name: 'Paraíba' },
  { uf: 'PR', name: 'Paraná' },
  { uf: 'PE', name: 'Pernambuco' },
  { uf: 'PI', name: 'Piauí' },
  { uf: 'RJ', name: 'Rio de Janeiro' },
  { uf: 'RN', name: 'Rio Grande do Norte' },
  { uf: 'RS', name: 'Rio Grande do Sul' },
  { uf: 'RO', name: 'Rondônia' },
  { uf: 'RR', name: 'Roraima' },
  { uf: 'SC', name: 'Santa Catarina' },
  { uf: 'SP', name: 'São Paulo' },
  { uf: 'SE', name: 'Sergipe' },
  { uf: 'TO', name: 'Tocantins' }
]


const mostrarPerfil = ref(false)

function handleFileUpload(e) {
  const target = e.target
  console.log(target)
  if (target && target.files) {
    const file = target.files[0]
    user.value.avatar = URL.createObjectURL(file)
  }
}

function salvarPerfil() {
  mostrarPerfil.value = true
}
</script>

<template>
  <div class="container">
   <form action="" class="form">
      <h1 class="title">{{ title }}</h1>
      <transition name="form" mode="out-in">
        <section v-if="mostrarPerfil">
          <div>
            <p v-for="(value, key) of user" :key="key">{{ key }}: {{ value }}</p>
          </div>
          <button class="btn btn-info" @click="mostrarPerfil = false">Esconder</button>
        </section>
        <form v-else class="row g-3 was-validated" @submit.prevent="salvarPerfil()" validate>
          <div>
            <label for="nomeField" class="form-label">Nome</label>
            <input type="text" class="form-control" id="nomeField" v-model="user.nome" required />
          </div>
          <div>
            <label for="sobrenomeField" class="form-label">Sobrenome</label>
            <input
              type="text"
              class="form-control"
              id="sobrenomeField"
              v-model="user.sobrenome"
              required
            />
          </div>
          <div>
            <label for="dataField" class="form-label">Data</label>
            <input type="datetime-local" class="form-control" id="dataField" v-model="user.data" required ></div>
          <div>
            <label for="emailField" class="form-label">E-mail @</label>
            <div class="input-group">
              <span class="input-group-text" id="emailFieldPrepend"></span>
              <input
                type="email"
                class="form-control"
                id="emailField"
                aria-describedby="emailFieldPrepend"
                v-model="user.email"
                required
              />
            </div>
          </div>
          <div>
            <label for="senhaField" class="form-label">Senha</label>
            <input type="text" class="form-control" id="senhaField" v-model="user.senha" />
          </div>
          <div>
            <label for="senhaconfirmField" class="form-label">Confirmar senha</label>
            <input type="text" class="form-control" id="senhaconfirmField" v-model="user.senhaconfirm" />
          </div>
          <div>
            <label for="cidadeField" class="form-label">Cidade</label>
            <input type="text" class="form-control" id="cidadeField" v-model="user.cidade" />
          </div>
          <div>
            <label for="estadoField" class="form-label">Estado</label>
            <select class="form-select" id="estadoField" v-model="user.estado">
              <option selected disabled value="">Selecionar...</option>
              <option v-for="estado of estados" :key="estado.uf" :value="estado.uf">
                {{ estado.name }}
              </option>
            </select>
          </div>
          
          <div>
            <label for="ruaField" class="form-label">Rua:</label>
            <input type="text" class="form-control" id="ruaField" v-model="user.rua" />
          </div>
          <div>
            <label for="bairroField" class="form-label">Bairro</label>
            <input type="text" class="form-control" id="bairroField" v-model="user.bairro" />
          </div>
          <div>
            <label for="biografiaField" class="form-label">Biografia</label>
            <input type="text" class="form-control" id="biografiaField" v-model="user.biografia" />
          </div>
          <div >
            <p>Hobbies</p>
            <div class="row-selection"><label for="hobbiesField">Esportes</label><input
              type="checkbox"
              id="hobbiesField"
              value="esportes"
              v-model="user.hobbies"
            /></div>
            <div class="row-selection"><label for="hobbiesField">Música</label><input
              type="checkbox"
              id="hobbiesField"
              value="música"
              v-model="user.hobbies"
            /></div>
            <div class="row-selection"><label for="hobbiesField">Viagens</label><input
              type="checkbox"
              id="hobbiesField"
              value="viagens"
              v-model="user.hobbies"
            />
            </div>
            <div class="row-selection"><label for="hobbiesField">Leitura</label><input
              type="checkbox"
              id="hobbiesField"
              value="leitura"
              v-model="user.hobbies"
            /></div>
          </div>
          <div >
            <p>Linguagem preferida</p>
            <div class="row-selection"><label for="langC">C</label><input
              type="radio"
              v-model="user.linguagempref"
              value="C"
              id="langC"
            /></div>
            <div class="row-selection"><label for="langJava">Java</label><input
              type="radio"
              v-model="user.linguagempref"
              value="Java"
              id="langJava"
            /></div>
            <div class="row-selection"><label for="langPython">Python</label><input
              type="radio"
              v-model="user.linguagempref"
              value="Python"
              id="langPython"
            /></div>
            <div class="row-selection">
              <label for="langJs">JavaScript</label><input
              type="radio"
              v-model="user.linguagempref"
              value="Javascript"
              id="langJs"
            /></div>
          </div>
          <div>
            <button  type="submit">Enviar</button>
          </div>
        </form>
      </transition>
    </form>
  </div>
</template>



<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Work+Sans:ital,wght@0,100..900;1,100..900&display=swap");

.container {
  height: auto;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  background-image: url("/fundo.avif");
  background-repeat: no-repeat ;
  background-size: cover;
}

.title {
  text-align: center;
  margin: 0px 0px 30px 0px;
}

h1 {
  font-family: "Work sans";
  font-weight: bold;
  color: aliceblue;
}

p{
  display: flex;
  align-self: flex-start;
  font-family: "Work sans";
  margin: 0px 0px 12px 13px;
  font-size: 23px;
  font-weight: bold;
}

form {
  font-family: "Work sans";
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: fit-content;
  width: 550px;
  padding: 40px;
  background-color: rgba(20, 18, 18, 0.527);
  border-radius: 30px;
  margin: 10px 50px 10px 50px;
  box-shadow: 1px 1px 10px 1px rgba(0, 0, 0, 0.3);
  color: aliceblue;
  display: grid;
  grid-template-areas: "main";
}


input {
  height: 35px;
  width: 200px;
  border-radius: 10px;
  border-color: #bab3ab;
  font-family: "Work sans";
  margin-top: 0;
  padding: 0px 0px 0px 10px;
}

label {
  display: flex;
  align-self: flex-start;
  font-family: "Work sans";
  margin-bottom: 10px;
  font-size: 1rem;
  font-weight: bold;
}

select {
  width: 120px;
  height: 30px;
  border-radius: 5px;
  font-family: "Work sans";
  align-self: flex-start;
  margin: 2px 10px 15px 13px;
}

.prog {
  display: flex;
  flex-direction: row;
}

#programmingLanguages {
  width: 148px;
  align-self: baseline;
  margin-right: 0;
}

.add-programming-languages-btn {
  margin: 2px 10px 0px 2px;
  width: 50px;
  height: 38px;
  border-color: #bab3ab;
  cursor: pointer;
  transition: 100ms ease-out;
}

.add-programming-languages-btn:hover {
  transform: scale(1.05);
  transition: 100ms ease-out;
  border-color: green;
}

.add-programming-languages-btn:active {
  transform: scale(1.2);
  transition: 100ms;
}

.show-result-bnt {
  align-self: center;
  cursor: pointer;
}

ul {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  margin: 0px 0px 0px 15px;
  width: 100%;
  font-size: 0.9rem;
}

li {
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  list-style: none;
  font-family: "Work sans";
  width: 100%;
  height: 30px;
  align-self: flex-start;
}

button {
  margin: 0 30px;
  border: 0;
  height: fit-content;
  width: fit-content;
  cursor: pointer;
  align-self: end;
  font-family: "Work sans";
  font-size: 1rem;
  transition: 100ms ease-in-out;
  font-weight: bold;
}

button:hover {
  transform: scale(1.2);
  transition: 100ms ease-in-out;
  color: rgb(160, 0, 0);
}

textarea {
  border-radius: 10px;
  border-color: #bab3ab;
  font-family: "Work sans";
  margin: 2px 10px 15px 10px;
  padding: 5px 0px 0px 5px;
}

#results-form > p {
  margin: 10px 0 0 0;
  word-break: normal;
}

.result-item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.result-item p {
  margin-right: .3em;
}
.row-selection{
  display: flex;
  justify-content: center;
  align-items: center;
}
.row-selection > label{
  width: 20%;
}
</style>
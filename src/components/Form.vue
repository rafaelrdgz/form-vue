<script setup>
  import {ref} from "vue";

  const name = ref("")
  const email = ref("")
  const age = ref()
  const sport = ref("")
  const checkedCareers = ref([])
  const recommendToStudy = ref("Definitivamente si")
  const comments = ref("")

  const errorMessage = (className) => {
    let container = document.querySelector(className)
    let p = container.querySelector('p')

    if(!p){
      p = document.createElement('p')
      p.style.color = "red"
      p.style.marginTop = "0.5rem"
      container.appendChild(p)
    }else{
      p.innerHTML = ""
    }

    return p
  }

  const isValidName = (name) =>{
    const regex = /^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]+$/;
    const p = errorMessage(".name-group")

    if (name.length < 10)
      return p.innerHTML = p.innerHTML + "El nombre debe tener al menos 10 caracteres."

    if (!name.match(regex))
      return p.innerHTML = p.innerHTML + "<br>El nombre solo puede contener caracteres alfabeticos."
  }

  const isValidEmail = (email) => {
    const regex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    const p = errorMessage(".email-group")

    if (!email)
      return p.innerHTML = p.innerHTML + "Por favor, inserte su email."

    if (!email.match(regex))
      return p.innerHTML = p.innerHTML + "Direccion de correo no valida."
  }

  const isValidAge =(age) =>{
    const p = errorMessage(".age-group")

    if (!age)
      return p.innerHTML = p.innerHTML + "Por favor, inserte su edad."

    if(age < 10 || age > 99)
      return p.innerHTML = p.innerHTML + "La edad debe corresponder al rango 10 - 99."
  }

  const errorMessageAddP = (className) => {
    let container = document.querySelector(className)
    let lastChild = container.lastElementChild

    if (lastChild.tagName === 'P'){
      lastChild.innerHTML = ""
      return lastChild
    }else{
      let p = document.createElement('p')
      p.style.color = "red"
      p.style.marginTop = "0px"
      lastChild.insertAdjacentElement('afterend', p)
      return p
    }
  }
  
  const isValidSport = (sport) => {
    const p = errorMessageAddP(".sport-group")

    if(!sport)
      return p.innerHTML = p.innerHTML + "<br>Por favor, seleccione un deporte."
  }

  const isValidCheckedCareers =(checkedCareers) =>{
    const p = errorMessageAddP(".careers-group")
    if (checkedCareers.length === 0)
      return  p.innerHTML = p.innerHTML + "<br>Por favor, seleccione al menos una carrera de su gusto."
  }

  function correctSubmit() {
    isValidName(name.value)
    isValidEmail(email.value)
    isValidAge(age.value)
    isValidSport(sport.value)
    isValidCheckedCareers(checkedCareers.value)
  }
</script>

<template>
  <div class="form">
    <div  class="form-group name-group">
      <label for="name">Nombre</label>
      <input class="form-input" v-model="name" type="text" placeholder="Inserta tu nombre">
    </div>
    <div class="form-group email-group">
      <label for="email">Correo</label>
      <input class="form-input" v-model="email" type="text" placeholder="Inserta tu correo">
    </div>
    <div class="form-group age-group">
      <label for="name">Edad</label>
      <input class="form-input" v-model="age" type="number" min="10" max="100" placeholder="Edad">
    </div>
    <div class="form-group sport-group">
      <p>Que deporte es de tu agrado?</p>
      <select class="form-select" v-model="sport" name="deporte">
        <option disabled value="">Selecciona un deporte</option>
        <option value="futbol">Futbol</option>
        <option value="atletismo">Atletismo</option>
        <option value="besibol">Beisbol</option>
        <option value="ajedrez">Ajedrez</option>
      </select>
    </div>
    <div class="form-group">
      <p>Recomendarias a un amigo que estudie en la CUJAE?</p>
      <label for="Definitivamente si">
        <input type="radio" v-model="recommendToStudy" name="user-recommend" value="Definitivamente si" checked>Definitivamente si
      </label>
      <label for="Quizas">
        <input type="radio" v-model="recommendToStudy" name="user-recommend" value="Quizas">Quizas
      </label>
      <label for="No estoy seguro">
        <input type="radio" v-model="recommendToStudy" name="user-recommend" value="No estoy seguro">No estoy seguro
      </label>
    </div>
    <div class="form-group careers-group">
      <p>Que carreras son de tu agrado?</p>
      <label for="Mecanica">
        <input v-model="checkedCareers" value="Mecanica" type="checkbox" name="prefer">Mecanica
      </label>
      <label for="Informatica">
        <input v-model="checkedCareers" value="Informatica" type="checkbox" name="prefer">Informatica
      </label>
      <label for="Telecomunicaciones">
        <input v-model="checkedCareers" value="Telecomunicaciones" type="checkbox" name="prefer">Telecomunicaciones
      </label>
      <label for="Civil">
        <input v-model="checkedCareers" value="Civil" type="checkbox" name="prefer">Civil
      </label>
      <label for="Electrica">
        <input v-model="checkedCareers" value="Electrica" type="checkbox" name="prefer">Electrica
      </label>
      <label for="Automatica">
        <input v-model="checkedCareers" value="Automatica" type="checkbox" name="prefer">Automatica
      </label>
    </div>
    <div class="form-group">
      <p>Tienes algun comentario o sugerencia?</p>
      <textarea class="form-textArea" v-model="comments" name="comments" placeholder="Escribe aqui tu comentario" ></textarea>
    </div>
    <button class="submit-btn" @click="correctSubmit" type="submit">Enviar</button>
  </div>
</template>

<style scoped>
.form{
  background-color: rgb(32, 41, 94, 0.5);
  border-radius: 10px;
  padding: 3rem;
}
.form-textArea{
  width: 100%;
  min-height: 6rem;
  resize: vertical;
}
.form p{
  margin-bottom: 1rem;
}
label, p, button{
  font-size: 1.5rem;
}
.form input textarea select{
  font-size: 1rem;
}
label{
  display: flex;
  margin-bottom: 0.2rem;
}
.form-group{
  margin-top: 0.8rem;
}
.form-input{
  width: 100%;
  height: 1.5rem;
  padding: 0.3rem;
  border-radius: 0.25rem;
  outline: none;
}
.form-select{
  width: 100%;
  height: 2.5rem;
  border-radius: 0.25rem;
  outline: none;
}
.submit-btn{
  background-color: springgreen;
  margin-top: 1rem;
  height: 2.5rem;
  width: 100%;
}
</style>
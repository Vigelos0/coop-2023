<script setup>
import { inject, reactive } from 'vue'
const router = inject('router');

let member = reactive({
    fullname: '',
    email: '',
    password: ''
})

function validationFormulaire() {
    api.post('members', {
        body: member
    }).then(response => {
        if (response.message) {
            alert(response.message)
        } else {
            console.log(response)

            if (confirm("Votre compte a été créé. Voulez-vous vous connecter ? ")) {
                // rediriger vers la route /se-connecter
                router.push('/se-connecter');
            }
        }
    })
}

</script>
<template>
  <div class="columns is-centered">
    <div class="column is-6">
      <div class="box">
        <h1 class="title has-text-centered">Créer un compte</h1>
        <form @submit.prevent="validationFormulaire">
          <div class="field">
            <label class="label">Nom</label>
            <div class="control">
              <input class="input" v-model="member.fullname" type="text" placeholder="Nom complet ou pseudonyme">
            </div>
          </div>
          <div class="field">
            <label class="label">E-Mail</label>
            <div class="control">
              <input class="input" v-model="member.email" type="email" placeholder="email@domaine.com">
            </div>
          </div>
          <div class="field">
            <label class="label">Mot de passe</label>
            <div class="control">
              <input class="input" v-model="member.password" type="password" placeholder="your password">
            </div>
          </div>
          <div class="field is-grouped is-grouped-centered">
            <div class="control">
              <button class="button is-primary">Créer un compte</button>
            </div>
            <div class="control">
              <router-link to="/se-connecter" class="button is-light">Annuler</router-link>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

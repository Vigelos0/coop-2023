<script setup>
import { inject, reactive } from 'vue'
const router = inject('router');
const session = inject('session');

let member = reactive({
    email: 'netlify@gmail.com',
    password: 'netlify'
})

function validationFormulaire() {
    api.post('members/signin', {
        body: member
    }).then(response => {
        if (response.message) {
            alert(response.message)
        } else {
            session.setSession(response.member, response.token);
            router.push('/');
        }
    })
}
</script>
<template>
    <div class="columns">
        <div class="column is-4 is-offset-4">

            <form class="box" @submit.prevent="validationFormulaire">

            <h1 class="title has-text-centered">SE CONNECTER</h1>

                <div class="field">
                    <label class="label">E-Mail</label>
                    <input class="input" v-model="member.email" type="email" placeholder="email@domaine.com">
                </div>

                <div class="field">
                    <label class="label">Mot de passe</label>
                    <input class="input" v-model="member.password" type="password">
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-primary">Se connecter</button>
                    </div>
                    <div class="control">
                        <router-link to="/" class="button">Annuler</router-link>
                    </div>
                </div>
            </form>
            <router-link to="/creer-un-compte">Créer un compte</router-link>


        </div>
    </div>

</template>

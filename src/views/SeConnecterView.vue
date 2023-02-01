<script setup>
import { inject, reactive } from 'vue'
const router = inject('router');
const session = inject('session');

let member = reactive({
    email: 'netlify@gmail.com',
    password: ''
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
    <div class="columns is-centered">
        <div class="column is-5">
            <div class="box">
                <h1 class="title has-text-center">Se connecter</h1>

                <form @submit.prevent="validationFormulaire">
                    <div class="form-group">
                        <label class="label">E-Mail</label>
                        <div class="control">
                            <input class="input" v-model="member.email" type="email" placeholder="email@domaine.com">
                        </div>
                    </div>

                    <div class="form-group">
                        <label class="label">Mot de passe</label>
                        <div class="control">
                            <input class="input" v-model="member.password" type="password" placeholder="your password">
                        </div>
                    </div>

                    <div class="form-group text-center">
                        <div class="btn-group">
                            <button class="btn">Se connecter</button>
                            <router-link to="/" class="btn">Annuler</router-link>
                        </div>
                    </div>
                </form>
            </div>

            <p class="text-center">
                <router-link to="/creer-un-compte" class="btn btn-primary">Créer un compte</router-link>
            </p>
        </div>
    </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

body {
  font-family: 'Poppins', sans-serif;
}

.columns {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 90vh;
}

.column {
  width: 100%;
  max-width: 576px;
}

.control {
    width: 100%;
}

.box {
  background-color: #fff;
  border-radius: 10px;
  padding: 30px;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
  text-align: center;
}

.title {
  font-size: 32px;
  margin-bottom: 30px;
  color: #333;
}

.form-group {
  margin-bottom: 30px;
  text-align: left;
}

.label {
  font-size: 16px;
  font-weight: 700;
  color: #333;
  margin-bottom: 10px;
  display: block;
}

.input {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
  width: 95%;
  font-size: 16px;
  color: #333;
  box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
}

.btn-group {
  display: flex;
  justify-content: center;
}

.btn {
  background-color: rgb(0, 94, 245);
  color: #fff;
  padding: 10px 20px;
  border-radius: 5px;
  text-decoration: none;
  font-size: 16px;
  font-weight: 700;
  margin: 0 10px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
  border: 1px solid rgb(0, 94, 245);
}

.btn:hover {
  background-color: #fff;
  color: rgb(0, 94, 245);
  border: 1px solid rgb(0, 94, 245);
}

.text-center {
  text-align: center;
}

.btn-primary {
  display: inline-block;
}

@media (max-width: 767px) {
  .column {
    width: 100%;
    max-width: none;
  }

  .box {
    padding: 20px;
  }

  .title {
    font-size: 24px;
  }

  .label {
    font-size: 14px;
  }

  .input {
    font-size: 14px;
  }

  .btn {
    font-size: 14px;
    padding: 8px 16px;
  }
}

</style>

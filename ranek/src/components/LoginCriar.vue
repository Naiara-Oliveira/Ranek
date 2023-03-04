<template>
    <section>
        <h2>Crie sua conta</h2>
        <transition mode="out-in">
            <button v-if="!criarConta" class="btn" @click="criarConta = true">Criar Conta</button>
            <UsuarioForm v-else>
                <button class="btn btn-form" @click.prevent="criarUsuario">Criar Usuário</button>
            </UsuarioForm>
        </transition>
    </section>
</template>

<script>
import UsuarioForm from "@/components/UsuarioForm.vue";
export default {
    name: "LoginCriar",
    data() {
        return {
            criarConta: false
        }
    },
    components: {
        UsuarioForm
    },
    methods: {
        async criarUsuario() {
            try{
            await this.$store.dispatch('criarUsuario', this.$store.state.usuario);
            await this.$store.dispatch("getUsuario", this.$store.state.usuario.email);
            this.$router.push({name: "usuario"});
            } catch (e) {
                console.log(e);
            }
        }
    }
}
</script>

<style scoped>
h2 {
    text-align: center;
    margin-top: 40px;
    margin-bottom: 10px;
}

.btn {
    margin-top: 10px;
    margin-left: auto;
    margin-right: auto;
    width: 100%;
    max-width: 300px;
}

.btn-form {
    margin-top: 10px;
    max-width: 100%;
}
</style>

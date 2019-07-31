<template>
  <q-page padding>
    <h3>Formulário</h3>

    <q-form @submit="save" @reset="reset" class="q-gutter-md">

      <q-input outlined v-model="user.name" label="Nome"
        hint="Obrigatório, precisa ter 3 ou mais caracteres"
        :rules="[
          val => !!val || 'Campo obrigatório',
          val => val.length > 2 || 'O seu nome é muito curto'
        ]">
        <template v-slot:prepend>
          <q-icon name="label"/>
        </template>
        <template v-slot:append>
          <q-icon name="account_box"/>
        </template>
      </q-input>

      <q-input outlined v-model="user.email" label="Email"
        :rules="[
          val => !!val || 'Campo obrigatório',
          val => /^[a-zA-Z.\-_]+@[a-zA-Z]+\.[a-z]+[a-zA-Z.]*$/.test(val) || 'Email inválido'
        ]">
        <template v-slot:prepend>
          <q-icon name="email"/>
        </template>
        <template v-slot:append>
          <q-icon name="account_box"/>
        </template>
      </q-input>

      <p>
        <q-toggle
        v-model="user.newsletter"
        label="Aceita receber novidades do canal?"
        color="red"
        checked-icon="check"
        unchecked-icon="clear"
        />
      </p>

      <q-btn type="submit" color="primary">Salvar</q-btn>
      <q-btn type="reset" color="secondary" class="q-ml-sm">Resetar</q-btn>
    </q-form>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      user: {
        newsletter: true,
      },
    };
  },
  methods: {
    save() {
      this.$q.notify({
        message: `Salvo com sucesso - <strong>${this.user.name}</strong>`,
        html: true,
      });
    },
    reset() {
      this.user = {
        newsletter: true,
      };
    }
  },
  mounted() {
    this.$q.notify.setDefaults({
      position: 'bottom-right',
      color: 'blue'
    });
  }
}
</script>

<style>
</style>

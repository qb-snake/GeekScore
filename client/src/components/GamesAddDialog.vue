<template>
  <BaseDialog activator-icon="plus" header="Add new game" @submit="submitGame">
    <v-text-field
      v-model.trim="name"
      clearable
      :rules="nameRules"
      prepend-icon="mdi-dice-multiple-outline"
      label="Name"
    />
    <v-switch
      v-model="coop"
      label="Cooperative"
      color="secondary"
      hide-details
    />
  </BaseDialog>
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from '@vue/composition-api'
import { standardField, requiredField } from '@/use/validations'

export default defineComponent({
  name: 'GamesAddDialog',
  setup(_, ctx) {
    const store = ctx.root.$store

    const state = reactive({
      name: '',
      coop: false,
      nameRules: [...standardField, requiredField]
    })

    const createGame = () => {
      const game = {
        coop: state.coop,
        name: state.name
      }
      store.dispatch('games/createGame', game)
    }

    const submitGame = () => {
      createGame()
      state.name = ''
    }

    return {
      submitGame,
      ...toRefs(state)
    }
  }
})
</script>

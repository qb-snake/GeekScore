<template>
  <BaseDialog
    activator-icon="pencil-outline"
    color="#607d8b"
    header="Edit round info"
    simple
    @submit="submitRound"
  >
    <v-switch
      v-model="toDelete"
      label="Delete round"
      color="error"
      hide-details
    />
  </BaseDialog>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  name: 'RoundsEditDialog',
  props: {
    round: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      toDelete: false
    }
  },
  methods: {
    ...mapActions('rounds', ['deleteRound']),
    submitRound() {
      if (this.toDelete) {
        this.deleteRound(this.round._id)
      }
    }
  }
}
</script>

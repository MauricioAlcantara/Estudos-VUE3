<template>
  <div class="notificacoes">
    <article
        class="message"
        :class="contexto[notificacao.tipo]"
        v-for="notificacao in notificacoes"
        :key="notificacao.id"
    >
      <div class="message-header">
        {{ notificacao.titulo }}
      </div>
      <div class="message-body">
        {{ notificacao.texto }}
      </div>
    </article>
  </div>
</template>

<script lang="ts">
import {computed, defineComponent} from "vue";
import {useStore} from "@/store";
import {TipoNoficacao} from "@/Interfaces/INotificacao";

export default defineComponent({
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Notificacoes',
  data () {
    return {
      contexto: {
        [TipoNoficacao.SUCESSO]: 'is-success',
        [TipoNoficacao.ATENCAO]: 'is-warning',
        [TipoNoficacao.FALHA]: 'is-danger',
      }
    }
  },
  setup () {
    const store = useStore()
    return {
      notificacoes: computed(() => store.state.notificacoes)
    }
  }
})

</script>

<style scoped>
.notificacoes {
  position: absolute;
  right: 0;
  width: 300px;
  padding: 8px;
  z-index: 105;
}
</style>
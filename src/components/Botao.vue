<template>
    <!-- <button @click="iniciar" :disabled="cronometroRodando" class="button"> -->
    <button @click="clicou" class="button">
        <span class="icon">
            <i :class="['fas', 'fa-' + nomeBotao]"></i>
        </span>
        <span>{{ nomeBotao }}</span>
    </button>
</template>

<script lang="ts">

import { defineComponent } from 'vue';


export default defineComponent({
    data() {
        return {
            nomeClass: ''
        }
    },
    props: {
        nomeBotao: {
            type: String,
            default: ''
        },
    },
    methods: {
        clicou() {
            this.$emit('clicou', { nome: this.nomeBotao })
        }
    }
})

</script>
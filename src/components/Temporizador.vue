<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Cronometro :tempoEmSegundos="tempoEmSegundos" />
        <Botao :nomeBotao="play" @clicou="testeClicou" :disabled="cronometroRodando"/>
        <Botao :nomeBotao="stop" @clicou="testeClicou" :disabled="!cronometroRodando" />
    </div>
</template>
  
<script lang="ts">
import { defineComponent } from "vue";
import Botao from "./Botao.vue";
import Cronometro from './Cronometro.vue'
export default defineComponent({
    name: "Temporizador",
    emits: ['aoTemporizadorFinalizado'],
    components: {
        Cronometro,
        Botao
    },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
            play: 'play',
            stop: 'stop'
        }
    },
    methods: {

        testeClicou(data: any): void {
            if (data.nome === 'play') {

                // começar a contagem
                // 1 seg = 1000 ms
                this.cronometroRodando = true
                this.cronometro = setInterval(() => {
                    this.tempoEmSegundos += 1
                }, 1000)
            }

            if (data.nome === 'stop') {
                this.cronometroRodando = false
                clearInterval(this.cronometro)
                this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
                this.tempoEmSegundos = 0
            }
        }
    }
});
</script>
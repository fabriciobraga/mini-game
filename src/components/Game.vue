<template>
  <v-container>
    <v-row class="text-center">
      
      <v-col cols="12 pt-8 title">
        Bem-vindo ao minigame!
      </v-col>

      <v-col cols="12" class="pb-0">
        <v-stepper v-model="stepper">
            <v-stepper-header>
            <v-stepper-step step="1">
                Questão 1
            </v-stepper-step>

            <v-divider></v-divider>

            <v-stepper-step step="2">
                Questão 2
            </v-stepper-step>

            <v-divider></v-divider>

            <v-stepper-step step="3">
                Questão 3
            </v-stepper-step>
            </v-stepper-header>
        </v-stepper>
      </v-col>

      <v-col cols="12" class="pt-1" v-for="step in steps" :key="step.indice">

          <v-expand-transition>
            <v-sheet v-if="stepper == step.indice && !step.showResultado" class="mt-6">
                <v-row>
                    <v-col cols="12">
                        <v-card class="elevation-10">
                            <v-card-text class="title">
                                {{step.pergunta}} {{step.indice}}
                            </v-card-text>
                        </v-card>
                    </v-col>

                    <v-col cols="12" v-for="resposta in step.respostas" :key="resposta.indice">
                        <v-card class="elevation-5">
                            <v-card-text class="title px-0 pa-0">
                                <v-btn :color="step.selecionado == resposta.indice ? 'blue lighten-2' : 'blue lighten-4'" 
                                    width="100%" @click="step.selecionado = resposta.indice" height="50">
                                    {{resposta.texto}}
                                    <v-icon right v-if="step.selecionado == resposta.indice">mdi-check</v-icon>
                                </v-btn>
                            </v-card-text>
                        </v-card>
                    </v-col>

                    <v-col cols="12" class="text-right">
                        <v-btn color="primary" class="mr-5" :disabled="step.selecionado == null" @click="step.showResultado = true;">
                            Responder
                        </v-btn>
                        <v-btn color="primary" class="" text outlined @click="restart">
                            Reiniciar
                        </v-btn>
                    </v-col>
                </v-row>
            </v-sheet>
          </v-expand-transition>
          <v-expand-transition>
            <v-sheet v-if="stepper == step.indice && step.showResultado" class="mt-6">
                <v-row>
                    <v-col cols="12">
                        <v-card class="elevation-10">
                            <v-card-title class="" v-bind:class="step.respostas[step.selecionado].resultado ? 'primary' : 'error'">
                                <v-spacer></v-spacer>
                                <v-icon large color="white" v-if="step.respostas[step.selecionado].resultado">mdi-emoticon-happy-outline</v-icon>
                                <v-icon large color="white" v-if="!step.respostas[step.selecionado].resultado">mdi-emoticon-sad-outline</v-icon>
                            </v-card-title>
                            <v-card-text class="title pa-5">
                                {{step.respostas[step.selecionado].mensagem}}
                            </v-card-text>
                        </v-card>
                    </v-col>
                    <v-col cols="12" class="text-right">
                        <v-btn v-if="step.respostas[step.selecionado].resultado && stepper < steps.length" class="mr-5 primary" @click="stepper += 1;">
                            Próxima
                        </v-btn>
                        <v-btn color="primary" class="" text outlined @click="restart">
                            Reiniciar
                        </v-btn>
                    </v-col>
                </v-row>
            </v-sheet>
          </v-expand-transition>
          
      </v-col>


    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      
        stepper : 1,

        pergunta1 : null,
        pergunta2 : null,
        pergunta3 : null,

        // array contendo os passos, perguntas e repostas
        //para adicionar mais opções ou remover, basta editar aqui
        steps : [
            {
                indice : 1,
                pergunta : 'Você acordou na floresta tonto e com uma grande dor de cabeça, sem nenhuma memória de como foi parar ali. Um barulho cada vez mais intenso foi o que despertou você desse apagão. Após abrir os olhos e levantar-se, você observa uma manada de búfalos vindo em sua direção, a pouquíssimos metros de distância. O que você faz?',
                selecionado : null,
                showResultado : false,
                respostas : [
                    {
                        indice : 0,
                        texto : 'Corre o mais rápido possível',
                        resultado : false,
                        mensagem : 'A sua corrida não foi suficiente para superar a da manada. Você morreu atropelado.'
                    },
                    {
                        indice : 1,
                        texto : 'Sobe na árvore',
                        resultado : true,
                        mensagem : 'Você sobe na árvore e escapa por pouco da manada.'
                    },
                    {
                        indice : 2,
                        texto : 'Se finge de morto',
                        resultado : false,
                        mensagem : 'Os búfalos podem até ter acreditado, mas isso não os impediu de passar por cima de você. Morreu atropelado.'
                    },
                ]
            },
            {
                indice : 2,
                pergunta : 'Ao ver que a manada passou, você desce da árvore e começa a explorar a região em busca de respostas. Não muito distante dali, você encontra um acampamento abandonado e um bilhete com instruções, deixado para trás. Antes que você possa alcançar o bilhete, um homem aparece com uma marreta gritando e avançando em sua direção. No seu corpo a adrenalina dispara. O que você faz?',
                selecionado : null,
                showResultado : false,
                respostas : [
                    {
                        indice : 0,
                        texto : 'Foge para bem longe',
                        resultado : false,
                        mensagem : 'Você consegue fugir do local e voltar à cidade, porém sem nenhuma ideia de quem o atacou. Você continua tentando juntar as peças do quebra-cabeças. 2 semanas depois você morre atropelado, “acidentalmente”,'
                    },
                    {
                        indice : 1,
                        texto : 'Pega o bilhete e foge para bem longe',
                        resultado : false,
                        mensagem : ' O homem lhe alcançou enquanto você tentava pegar o bilhete e lhe acertou uma marretada. Você morreu.'
                    },
                    {
                        indice : 2,
                        texto : 'Puxa toda coragem do coração e enfrenta o homem',
                        resultado : true,
                        mensagem : 'Você consegue desviar da primeira marretada do homem, que fica ocioso por um curto período, o suficiente para você acertá-lo em cheio na cabeça e apagá-lo no chão.'
                    },
                ]
            },
            {
                indice : 3,
                pergunta : 'Você finalmente consegue ler o bilhete: “Vamos fazer parecer um acidente. Misture o conteúdo deste frasco na comida dele. O remédio vai começar a fazer efeito depois de 30 minutos. Quando ele estiver completamente apagado, leve-o até o pé da árvore mais alta no início da floresta e direcione a manada de búfalos em sua direção. Estaremos esperando no laboratório ao norte do acampamento.” O que você faz?',
                selecionado : null,
                showResultado : false,
                respostas : [
                    {
                        indice : 0,
                        texto : 'Foge e liga para a polícia',
                        resultado : true,
                        mensagem : 'Você informa a polícia o que aconteceu e passa a localização do laboratório. Chegando lá ela se depara com um sítio de produção de cocaína e prende todos os presentes. As evidências sugerem que você ainda pode estar em perigo, por este motivo a polícia lhe coloca no programa de proteção à testemunha e você sobrevive para vivenciar uma nova história. Parabéns, você ganhou!'
                    },
                    {
                        indice : 1,
                        texto : 'Amarra o homem e vai ao laboratório',
                        resultado : false,
                        mensagem : ' Você amarra o homem e se dirige ao laboratório. Você entra silenciosamente e consegue chegar ao salão principal, onde você observa aproximadamente umas 10 pessoas. Um passo em falso entrega a sua posição e você é alvejado. Você morreu.'
                    },
                    {
                        indice : 2,
                        texto : 'Mata o homem, pega a marreta e vai ao laboratório',
                        resultado : false,
                        mensagem : 'Você mata o homem, pega a marreta e se dirige ao laboratório. Ao avistar 2 guardas na entrada, confiante de si e seus feitos recentes, você corre na direção dos guardas, segurando a marreta com as duas mãos levantadas acima da sua cabeça e gritando “LEEROY JEENKINS!!!!”. Infelizmente, o efeito surpresa foi prejudicado e os guardas não tiveram dificuldade em alvejá-lo. Você morreu.'
                    },
                ]
            },
        ]
    }),

    methods : {

        // processaResposta1(){
        //     if(pergunta1 == 0){

        //     }
        // },

        restart(){
            for (var i = 0; i < this.steps.length ; i++){
                this.steps[i].selecionado = null;
                this.steps[i].showResultado = false;
            }
            this.stepper = 1;
            
        }
    }
  }
</script>

<style>

/* your css */

.v-card__text, .v-card__title {
  word-break: normal; /* maybe !important  */
}

</style>

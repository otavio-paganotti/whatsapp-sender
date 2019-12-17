<template>
  <q-page class="">
    <div class="q-pa-md">
      <div class="q-col-gutter-md row">
        <div class="col-12 col-md-4 offset-4">
          <q-card>
            <q-card-section>
              <q-card-section>
                <div class="text-h6">Envio de mensagens em massa meio manual</div>
                <div class="text-subtitle2">by DouraSoft</div>
              </q-card-section>
            </q-card-section>

            <q-card-section>
              <div class="q-pa-md">
                <div class="q-col-gutter-md row">
                  <div class="col-12">
                    <q-input
                      v-model="numero.telefone"
                      filled
                      label="Telefone"
                    />
                  </div>
                  <div class="col-12">
                    <q-input
                      v-model="numero.msg"
                      filled
                      autogrow
                      counter
                      label="Conteúdo da mensagem"
                    />
                  </div>
                </div>
              </div>
            </q-card-section>

            <q-card-actions style="position:absolute;right: 0">
              <div class="q-pa-md">
                <div class="q-col-gutter-md row">
                  <div class="col-12">
                    <q-btn
                      label="+5567"
                      cliclable
                      @click="preenche(1)"
                      style="margin-right: 10px"
                    />
                    <q-btn
                      label="+55"
                      cliclable
                      @click="preenche(2)"
                      style="margin-right: 10px"
                    />
                    <q-btn
                      label="Tudo certo"
                      cliclable
                      @click="enviar"
                      color="green"
                      icon-right="send"
                    />
                  </div>
                </div>
              </div>
            </q-card-actions>
          </q-card>
        </div>
      </div>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
import axios from 'axios'
const moment = require('moment')
export default {
  name: 'HelloWorld',
  data: () => {
    return {
      numero: {
        msg: "Boa tarde. recebi seu contato pelo facebook, em relação a vaga de trabalho aqui na DouraSoft. Gostaria de saber se já acessou o link e preencheu seu currículo online. https://jobs.solides.com/dourasoft",
        telefone: "",
        enviadoem: ""
      }
    }
  },
  methods: {
    enviar () {
      //eslint-disable-next-line
      window.open('https://api.whatsapp.com/send?phone=' + this.numero.telefone + '&text=' + this.numero.msg.replace(/\ /g, '%20'), '_blank')
      this.saveLog(this.numero)
    },
    saveLog (num) {
      num.enviadoem = moment().format('DD/MM/YYYY HH:mm:ss')
      axios.post('http://localhost:3000/enviados', num)
        .then(() => {
          this.numero.telefone = ""
          this.numero.msg = "Boa tarde. recebi seu contato pelo facebook, em relação a vaga de trabalho aqui na DouraSoft. Gostaria de saber se já acessou o link e preencheu seu currículo online. https://jobs.solides.com/dourasoft"
        })
    },
    preenche (type) {
      if (type === 1) {
        this.numero.telefone = "+5567" + this.numero.telefone
      }
      if (type === 2) {
        this.numero.telefone = "+55" + this.numero.telefone
      }
      this.enviar()
    }
  }
}
</script>

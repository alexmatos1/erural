<template>
  <label style="margin-top: 40px; font-size: 20px;">Lista de Salas</label>
  <q-list bordered class="rounded-borders" style="max-width: 100%;margin-top: 20px; min-width: 600px;">
    <q-item-label header>Salas Disponíveis</q-item-label>

    <q-item v-for="(item, index) in salas">
      <q-item-section avatar top>
        <span class="material-icons size-icon"> 
          meeting_room
        </span>
      </q-item-section>

      <q-item-section top class="col-2 gt-sm">
        <q-item-label class="q-mt-sm">Sala {{index + 1}} </q-item-label>
      </q-item-section>

      <q-item-section top>
        <q-item-label lines="1">
          <span class="text-weight-medium">Criada por: {{item.criador}}</span>
          <!-- <span class="text-grey-8"> GitHub repository</span> -->
        </q-item-label>
        <q-item-label caption lines="1">
          Assunto: {{item.assunto}}
        </q-item-label>
      </q-item-section>

      <q-item-section top side>
        <div class="text-grey-8 q-gutter-xs">
          <q-btn class="gt-xs" label="Entrar" @click="salaSelecionada(index)" size="16px" flat dense round icon="login" />
          <!-- <q-btn class="gt-xs" size="12px" flat dense round icon="done" /> -->
          <!-- <q-btn size="12px" flat dense round icon="more_vert" /> -->
        </div>
      </q-item-section>

      <q-separator spaced />
    </q-item>
  </q-list>


  <q-dialog v-model="confirm" persistent  style="margin-top: 30px;">
      <q-card>
        <span class="q-ml-sm" style="font-size: 20px; font-weight: 700; margin-bottom: 80px">Cadastro de Salas</span>

        <q-card-section class="row items-center" style="margin-top: 30px;">
          <q-form
            class="q-gutter-md"
            style="width: 400px;" 

            >
            <q-input
              filled
              v-model="salaCriador"
              label="Criador da Sala *"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Informe o Criador da Sala']"
            />

            <q-input
              filled
              v-model="salaAssunto"
              label="Assunto *"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Informe o Assunto da Sala']"    
            />

            <q-input
              filled
              v-model="salaLink"
              label="Link do vídeo *"
              lazy-rules
              :rules="[ val => val && val.length > 0 || 'Informe o Link do Vídeo']"    
            />


            <div style="float: right;">
              <q-btn label="Salvar" color="primary" v-close-popup @click="addSala()"/>
              <q-btn label="Cancelar" color="primary" flat class="q-ml-sm" v-close-popup/>
            </div>
          </q-form>
        </q-card-section> 
      </q-card>
  </q-dialog>

  
  <q-page-sticky position="bottom-right" :offset="[18, 18]">
    <span style="font-weight: 700;">Nova sala </span>
            <q-btn fab icon="add" color="green" @click="mostarDialog()" />
  </q-page-sticky>





  <q-dialog
      v-model="dialog"
      persistent
      :maximized="maximizedToggle"
      transition-show="slide-up"
      transition-hide="slide-down"
    >
      <q-card v-model="salas"  class="bg-primary text-white">
        <q-bar>
          <q-space />

          <q-btn dense flat icon="minimize" @click="maximizedToggle = false" :disable="!maximizedToggle">
            <q-tooltip v-if="maximizedToggle" class="bg-white text-primary">Minimizar</q-tooltip>
          </q-btn>
          <q-btn dense flat icon="crop_square" @click="maximizedToggle = true" :disable="maximizedToggle">
            <q-tooltip v-if="!maximizedToggle" class="bg-white text-primary">Maximizar</q-tooltip>
          </q-btn>
          <q-btn dense flat icon="close" v-close-popup>
            <q-tooltip class="bg-white text-primary">Fechar</q-tooltip>
          </q-btn>
        </q-bar>

        <q-card-section>
          <div class="text-h6">{{salas[salaIndex].assunto}}</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          {{salas[salaIndex].criador}}
        </q-card-section>

        <q-video :ratio="16/7"
          :src="salas[salaIndex].link"
        />
      </q-card>
    </q-dialog>

</template>


<script>
import { ref } from 'vue'
import { useQuasar } from 'quasar'


export default {
  name: 'HelloWorld',

  setup() {
    return {
      //salaNome:ref(''),
      salaCriador:ref(''),
      salaAssunto:ref(''),
      salaLink:ref(''),
      
      salaIndex:ref(),

      confirm: ref(false),
      accept: ref(false),

      dialog: ref(false),
      maximizedToggle: ref(true),

      salas: ref([
        {
          //nome: 'O melhor carro do mundo é:',
          criador: 'Erural',
          assunto: 'Notícias Erural',
          link: 'https://www.youtube.com/embed/vnrnUDt68-8',
        },
        {
          //nome: 'A melhor comida mundo é:',
          criador: 'Erural',
          assunto: 'O poder do planejamento na pecuária!',
          link: 'https://www.youtube.com/embed/f38QtXWTqv8',
        },
        {
          //nome: 'O melhor Estado do Brasil é:',
          criador: 'Erural',
          assunto: 'Dicas',
          link: 'https://www.youtube.com/embed/ZyKp4ThJ53Y',
        }

      ]),
      reset() {
        this.step = 1,
          this.group1 = '',
          this.group2 = '',
          this.group3 = ''
      },

      addSala() {
        if((this.salaCriador && this.salaAssunto && this.salaLink) != ""){  
          this.salas.push({criador:this.salaCriador, assunto:this.salaAssunto, link:this.salaLink});
          this.salaCriador = '',
          this.salaAssunto = '',
          this.salaLink = ''
        }  
      },

      removerSala() {
        if((this.salaCriador && this.salaAssunto && this.salaLink) != ""){  
          this.salas.push({criador:this.salaCriador, assunto:this.salaAssunto, link:this.salaLink});
          console.log(this.salas)   
        }  
      },

      mostarDialog(){
        this.confirm = true;
      },

      salaSelecionada(index){ 
        console.log(index)
        this.dialog = true; 
        this.salaIndex = index;          
      }



    }
  }
}

</script>


<style>
.btn-reset {
  float: right;
  margin-top: 10px;
}

.size-icon {
  font-size: 40px !important;
  color: black !important;
}
.q-page-container{
  margin-top: 40px !important;
}
</style> 
<template>
  <v-container fluid>
      <v-form>
          <v-file-input 
          multiple 
          chips 
          v-model="files" 
          label="Selecione as legendas"
          prepend-icon="mdi-message-text"
          outlined
          append-outer-icon="mdi-send"
          @click:append-outer="processSubtitles"
          />

          
      </v-form>
      <div class="pills">
          <Pil v-for="word in  groupedWords" :key="word.name" :name="word.name" :amount="word.amount" />
      </div>
  </v-container>
</template>

<script>
import { ipcRenderer } from 'electron'
import Pil from './Pil'

export default {
    components: {
    Pil
  },
    data: function () {
        return {
            files: [],

            groupedWords: [
                { name: 'you', amount: 900 },
                { name: 'he', amount: 550 },
                { name: 'i', amount: 600 },
                
            ]
        }
    },
    methods: {
        processSubtitles(){
            console.log(this.files)

            ipcRenderer.send('blabla', 'ping')
            ipcRenderer.on('blabla', (event, resp) =>{
                console.log(resp)
            })
           
            }
        }
    }

</script>

<style>
.pills {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}
</style>
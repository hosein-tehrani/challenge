<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline">
          چالش تستی 
        </v-card-title>
        <v-card-text>
          <v-autocomplete placeholder="لطفا نام خود را وارد کنید" @input="onInput" :disabled='isBusy' :loading="isBusy" :items="items" dense outline v-model="input"></v-autocomplete>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import Axios from "axios";
export default {
  name: 'IndexPage',
  data(){
    return{
      input:'',
      items:[
          { text: 'حسین', value: 'hossein'},
          { text: 'علی', value: 'ali'},
          { text: 'سینا', value: 'sina'},
          { text: 'حسام', value: 'hesam'},
          { text: 'مهیار', value: 'mahyar'},        
      ],
      isBusy:false,
    }
  },
  methods:{
    onInput(e){
      setTimeout(() => {
      this.isBusy = true;
      Axios
        .post(
           "https://test/export",
          {
            input: e
          },
        )
        .then(res => {
          this.isBusy = false;
          alert(res);
        })
        .catch(err => {
          alert(err)
          this.isBusy = false;
        });        
      }, 1000);
    }
  }
}
</script>

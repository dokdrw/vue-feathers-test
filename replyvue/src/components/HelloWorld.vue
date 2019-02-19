<template>
  <!--//////////////////////////////////////////////////////////////////////////////////////////////-->
  <!--//////////////////////////////////////Data Table Test/////////////////////////////////////////-->
  <div class="divStyle1">
    <v-alert :value="alertaS" type="success">
      {{texto}}
    </v-alert>
    <v-alert :value="alertaW" type="info">
      {{texto}}
    </v-alert>
    <!--<v-img src="https://www.freeiconspng.com/uploads/green-leafs-png-5.png"></v-img>-->
    
    <v-container grid-list-xl text-xs-center fluid>
      <v-layout row wrap>
        <v-flex xs12>
          <v-card class="comboStyle">
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-select v-model="size" :items="items" label="grid-list-size"></v-select>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
    
    <v-container v-bind="{ [`grid-list-${size}`]: true }" text-xs-center>
      <v-layout row wrap>
        <v-flex xs12 sm12 md6 lg4>
          <v-card dark color="purple">
            <v-card-text>This is a testing text.</v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 sm12 md6 lg4>
          <v-card dark color="secondary">
            <v-card-text>This is other testing text.</v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 sm12 md6 lg4>
          <v-card dark color="green">
            <v-card-text>This is another testing text.</v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>

    <!--///////////////////////////////////////////////////////////////////////////////////////////////////////////-->
    <!--////////////////////////////////////////////Dialogo cargando////////////////////////////////////////////////-->
    <div class="text-xs-center">
      <v-btn :disabled="dialog1" :loading="dialog1" class="white--text" color="purple darken-2" @click="dialog1 = true">
        Start loading
      </v-btn>
      <v-container grid-list-xl text-xs-center xs12 sm10 md8 lg6>
        <v-layout row wrap justify-center>
          <v-flex xs12 sm5 md4 lg3>
            <v-card class="green darken-3 white--text">
              <v-card-text><span class="font-weight-thin">Delay time loading</span></v-card-text>
            </v-card>
          </v-flex>
          <v-flex xs12 sm5 md4 lg3>
            <v-card dark class="cardStyle">
              <!--<v-card-actions><input v-model="valor" type="number" class="white--text text--darken-2 body-2 
                grey darken-1 font-weight-thin font-italic inputStyle"></v-card-actions>-->
              <v-text-field v-model="valor" :rules="[rules.requerido, rules.counter, rules.numero]" label="(Segundos)" 
                counter maxlength="2" class="font-weight-thin font-italic inputStyle"></v-text-field>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
      
      <v-dialog v-model="dialog1" hide-overlay persistent width="300">
        <v-card dark>
          <v-card-text>
            Please stand by
            <v-progress-linear :value="valor" color="white" class="mb-0"></v-progress-linear>
          </v-card-text>
        </v-card>
      </v-dialog>
    </div>

    <!--///////////////////////////////////////////////////////////////////////////////////////////////////////////-->
    
    <v-app id="inspire" class="styleTable">
      <div>
        <v-toolbar flat color="white" class="styleTable">
          <v-toolbar-title>Data Table Test</v-toolbar-title>
          <v-divider
            class="mx-2"
            inset
            vertical
          ></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <v-btn slot="activator" color="primary" dark class="mb-2">New Item</v-btn>
            <v-card>
              <v-card-title>
                <span class="headline">{{ formTitle }}</span>
              </v-card-title>
    
              <v-card-text>
                <v-container grid-list-md>
                  <v-layout wrap>
                    <v-flex xs12 sm6 md4>
                      <v-text-field v-model="editedItem.name" label="Dessert name"></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm6 md4>
                      <v-text-field v-model="editedItem.calories" label="Calories"></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm6 md4>
                      <v-text-field v-model="editedItem.fat" label="Fat (g)"></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm6 md4>
                      <v-text-field v-model="editedItem.carbs" label="Carbs (g)"></v-text-field>
                    </v-flex>
                    <v-flex xs12 sm6 md4>
                      <v-text-field v-model="editedItem.protein" label="Protein (g)"></v-text-field>
                    </v-flex>
                  </v-layout>
                </v-container>
              </v-card-text>
    
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" flat @click="close">Cancel</v-btn>
                <v-btn color="blue darken-1" flat @click="save">Save</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
        <v-data-table
          :headers="headers"
          :items="desserts"
          class="elevation-1"
        >
          <template slot="items" slot-scope="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.calories }}</td>
            <td class="text-xs-right">{{ props.item.fat }}</td>
            <td class="text-xs-right">{{ props.item.carbs }}</td>
            <td class="text-xs-right">{{ props.item.protein }}</td>
            <td class="justify-center layout px-0">
              <v-icon
                small
                class="mr-2"
                @click="editItem(props.item)"
              >
                edit
              </v-icon>
              <v-icon
                small
                @click="deleteItem(props.item)"
              >
                delete
              </v-icon>
            </td>
          </template>
          <template slot="no-data">
            <v-btn color="primary" @click="initialize">Reset</v-btn>
          </template>
        </v-data-table>
      </div>
    </v-app>
  </div>
  <!--//////////////////////////////////////////////////////////////////////////////////////////////-->
  <!--//////////////////////////////////////////////////////////////////////////////////////////////-->

  <!--<v-container>
    <v-layout text-xs-center wrap>
      <v-flex xs12>

      </v-flex>
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        ></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to Vuetify
        </h1>
        <p class="subheading font-weight-regular">
          For help and collaboration with other Vuetify developers,
          <br>please join our online
          <a href="https://community.vuetifyjs.com" target="_blank">Discord Community</a>
        </p>
      </v-flex>

      <v-flex
        mb-5
        xs12
      >
        <h2 class="headline font-weight-bold mb-3">What's next?</h2>

        <v-layout justify-center>
          <a
            v-for="(next, i) in whatsNext"
            :key="i"
            :href="next.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ next.text }}
          </a>
        </v-layout>
      </v-flex>

      <v-flex
        xs12
        mb-5
      >
        <h2 class="headline font-weight-bold mb-3">Important Links</h2>

        <v-layout justify-center>
          <a
            v-for="(link, i) in importantLinks"
            :key="i"
            :href="link.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ link.text }}
          </a>
        </v-layout>
      </v-flex>

      <v-flex
        xs12
        mb-5
      >
        <h2 class="headline font-weight-bold mb-3">Ecosystem</h2>

        <v-layout justify-center>
          <a
            v-for="(eco, i) in ecosystem"
            :key="i"
            :href="eco.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ eco.text }}
          </a>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>-->
</template>

<style>
  .inputStyle {
    border-radius:2px;
  }
  .cardStyle {
    padding: 10px;
  }

  .divStyle1 {
    background-image: url("https://www.freeiconspng.com/uploads/green-leafs-png-5.png");
  }
  .styleTable {
    background-color: transparent !important;
    background: transparent !important;
  }
  .comboStyle {
    background: rgba(255,255,255,0.5) !important;
  }
</style>


<script>
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  ///////////////////////////////////////////Data Table Test////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  /*new Vue({
    el: '#app',
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Actions', value: 'name', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      },
      defaultItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      }
    },

    watch: {
      dialog (val) {
        val || this.close()
      }
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.desserts = [
          {
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3
          },
          {
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0
          },
          {
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3
          },
          {
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9
          },
          {
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0
          },
          {
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0
          },
          {
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5
          },
          {
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9
          },
          {
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7
          }
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.desserts.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
      },

      close () {
        this.dialog = false
        setTimeout(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        }, 300)
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      }
    }
  })*/
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////

  export default {
    name: 'hello',
    /*data: () => ({
      ecosystem: [
        {
          text: 'vuetify-loader',
          href: 'https://github.com/vuetifyjs/vuetify-loader'
        },
        {
          text: 'github',
          href: 'https://github.com/vuetifyjs/vuetify'
        },
        {
          text: 'awesome-vuetify',
          href: 'https://github.com/vuetifyjs/awesome-vuetify'
        }
      ],
      importantLinks: [
        {
          text: 'Documentation',
          href: 'https://vuetifyjs.com'
        },
        {
          text: 'Chat',
          href: 'https://community.vuetifyjs.com'
        },
        {
          text: 'Made with Vuetify',
          href: 'https://madewithvuetifyjs.com'
        },
        {
          text: 'Twitter',
          href: 'https://twitter.com/vuetifyjs'
        },
        {
          text: 'Articles',
          href: 'https://medium.com/vuetify'
        }
      ],
      whatsNext: [
        {
          text: 'Explore components',
          href: 'https://vuetifyjs.com/components/api-explorer'
        },
        {
          text: 'Select a layout',
          href: 'https://vuetifyjs.com/layout/pre-defined'
        },
        {
          text: 'Frequently Asked Questions',
          href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions'
        }

      ],
      messageService: undefined,
      response: []
    }),*/

  //////////////////////////////////////////////////////////////////////////////////////////////////////
  ///////////////////////////////////////////Data Table Test////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////

    //el: '#app',
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'Dessert (100g serving)',
          align: 'left',
          sortable: false,
          value: 'name'
        },
        { text: 'Calories', value: 'calories' },
        { text: 'Fat (g)', value: 'fat' },
        { text: 'Carbs (g)', value: 'carbs' },
        { text: 'Protein (g)', value: 'protein' },
        { text: 'Actions', value: 'name', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      },
      defaultItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0
      },
      texto: "Valor inicial",
      alertaS: true,
      alertaW: false,
      size: 'xl',
      items: [
        { text: 'Extra large (24px)', value: 'xl' },
        { text: 'Large (16px)', value: 'lg' },
        { text: 'Medium (8px)', value: 'md' },
        { text: 'Small (4px)', value: 'sm' },
        { text: 'Extra small (2px)', value: 'xs' }
      ],
      dialog1: false,
      valor: 10,
      rules: {
        requerido: value => !!value || 'Required.',
        counter: value => value.length <= 2 || 'Max 2 characters',
        numero: value => {
          const pattern = /^[0-9]*$/
          return pattern.test(value) || 'Invalid number.'
        }
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      }
    },

    watch: {
      dialog (val) {
        val || this.close()
      },

      dialog1 (val) {
        if (!val) return
        
        setTimeout(() => (this.dialog1 = false), this.valor*1000)
        //this.setvalor()
      }
    },
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////////////////////////////////////////////////////////////////
    beforeCreate(){
      //
    },
    created(){
      this.messageService = this.$feathers.service('messages');
      this.messageService.find({
        query: {}
      }).then( response => {
        this.response = response;
        
        ////////////////////////////////Obteniendo datos desde archivo.db/////////////////////////////////////////
        for(var i=0;i<response.data.length;i++){
          this.desserts.push(response.data[i].text)
        }
        //Modificando en valor de texto desde el servidor
        //this.texto = response.data[0].text +" "+ response.data[1].text +" "+ response.data[2].text
        /*response.limit = 100

        var t = 0;
        var k = {"name":"","calories":"","fat":"","carbs":"","protein":"",}
        for(var i=0;i<response.data.length;i++){
          //console.log(response.data[i].text.split(","))
          var j = response.data[i].text.split(",")
          if(j[0] == "name"){
            k.name = j[1]
          }else if(j[0] == "calories"){
            k.calories = j[1]
          }else if(j[0] == "fat"){
            k.fat = j[1]
          }else if(j[0] == "carbs"){
            k.carbs = j[1]
          }else if(j[0] == "protein"){
            k.protein = j[1]
          }

          if(t >= 4){
            console.log(k)
            this.desserts.push(k)
            t = 0;
            k = {"name":"","calories":"","fat":"","carbs":"","protein":"",}
          }else{
            t++;
          }
        }*/

        //this.desserts.push()

        console.log(response)
      }).catch( err =>{
        console.log(err)
      })
        ///////////////////////////////////////////////////////////////////////////////////////////////////////////
        //////////////////////////////////////////Part of Data Table///////////////////////////////////////////////
        this.initialize()
        ///////////////////////////////////////////////////////////////////////////////////////////////////////////
        ///////////////////////////////////////////////////////////////////////////////////////////////////////////
    },
    mounted(){
      // 
    },
    methods: {
  ///////////////////////////////////////////////////////////////////////////////////////////////////////////
  //////////////////////////////////////////Part of Data Table///////////////////////////////////////////////
      initialize () {
        this.desserts = [
          /*{
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3
          },
          {
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0
          },
          {
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3
          },
          {
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9
          },
          {
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0
          },
          {
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0
          },
          {
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5
          },
          {
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9
          },
          {
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7
          }*/
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.desserts.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
      },

      close () {
        this.dialog = false
        setTimeout(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        }, 300)
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)

          /////////////////////////////////////////////////////////////////////////////////////
          //////////////////////////////////Creando mensaje////////////////////////////////////
          
          this.texto = this.editedItem
          this.alertaS = false
          this.alertaW = true

          this.messageService.create({
            text: this.editedItem
          }).then( created =>{
            console.log(created)
          }).catch( err =>{
            
          })
          /*this.messageService.create({
            text: "name,"+ this.editedItem.name
          }).then( created =>{
            console.log(created)
          }).catch( err =>{
            
          })
          this.messageService.create({text: "calories,"+ this.editedItem.calories}).then( created =>{console.log(created)}).catch( err =>{})
          this.messageService.create({text: "fat,"+ this.editedItem.fat}).then( created =>{console.log(created)}).catch( err =>{})
          this.messageService.create({text: "carbs,"+ this.editedItem.carbs}).then( created =>{console.log(created)}).catch( err =>{})
          this.messageService.create({text: "protein,"+ this.editedItem.protein}).then( created =>{console.log(created)}).catch( err =>{})*/

          /////////////////////////////////////////////////////////////////////////////////////

        }
        this.close()
      }
  ///////////////////////////////////////////////////////////////////////////////////////////////////////////
  ///////////////////////////////////////////////////////////////////////////////////////////////////////////  

    }
  }
</script>

<style>

</style>

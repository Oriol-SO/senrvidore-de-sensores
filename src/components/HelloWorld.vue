<template>
  <v-container>
    <v-main class="">
          <v-container >
            <v-card color="#082b52" >
              <v-card-title style="color:#fff ;">
                Funcionamiento de motor y sensores con ESP32
              </v-card-title>  

            </v-card>
            <v-card class="mt-2 py-2" style="text-align: center;" elevation="0">
              <v-btn class="text-capitalize" small color="success" @click="botonOn()" >Encender led</v-btn>
              <v-btn class="text-capitalize" small color="error" @click="botonOff()" >Apangar led</v-btn>

            </v-card>
            <template>
              <v-card class="mt-2"  >
                <v-row>
                  <v-col cols="12" sm="8">
                      <!--div>
                        <v-card-title>
                          <v-card elevation="0" style="color:#1976d2" class="pr-5 py-1">
                            TEMPERATURA Y HUMEDAD
                          </v-card>
                          
                        </v-card-title>
                        <div class="mx-2 mb-2 ">
                          <v-row>
                            <v-col cols="12" sm="6">
                              <div>
                                <v-card elevation="0">
                                  <v-card-text 
                                  id="valortemp"
                                  >
                                    Temperatura:
                                    <v-chip
                                    color="warning"
                                    >
                                    {{temperatura}} °C
                                    </v-chip>
                                  </v-card-text>
                                  
                                </v-card>
                                <v-card elevation="0">
                                  <v-card-text>
                                    Humedad:
                                    <v-chip
                                    color="primary"
                                    >
                                    {{humedad}} %
                                    </v-chip>
                                  </v-card-text>                    
                                </v-card>
                              </div>
                            </v-col>
                            
                          </v-row>
                        </div>  
                        <v-card elevation="0" width="400">
                          <v-card-subtitle>
                            Agregar un parametro
                          </v-card-subtitle>
                          <div class="mx-3 ">
                            <v-row>
                              <v-col cols="12" sm="8">
                                <v-text-field
                                label="Valor entero"
                                v-model="limite"
                                v-bind:color="isNaN(limite)?'error':'primary'"
                                >
                                </v-text-field>
                                <small v-if="isNaN(limite)" style="color:red;">El parametro no es un número</small>
                              </v-col>
                              <v-col cols="12" sm="4" class="my-auto"  >
                                <v-card-actions>
                                  <v-btn
                                    class="primary"
                                    small
                                    class="text-capitalize"
                                    @click="enviarlimite()"
                                    v-bind:disabled="isNaN(limite)?true:false"
                                    >
                                      Enviar
                                    </v-btn>
                                
                                </v-card-actions>
                              </v-col>
                            </v-row>
                          
                            
                          </div>
                        </v-card> 
                      </div-->
                    <v-card elevation="0">
                      <v-card-title >
                        <v-card elevation="0" style="color:#1976d2" class="pr-5 py-1">
                         MOTOR
                        </v-card>
                        
                        <v-btn class="ml-2" small color="primary" @click="prendermotor()">PRENDER</v-btn>
                        <v-btn class="ml-2" small color="error" @click="apagarmotor()">APAGAR</v-btn>
                      </v-card-title>
                      <v-card-title  >
                        <v-card elevation="0" style="color:#1976d2" class="pr-5 py-1">
                          POTENCIÓMETRO
                        </v-card>
                      
                      </v-card-title>
                      <div class="d-flex" style="justify-content:center">
                        <v-card style="width: 70%;" color="#dcdfe5a6">
                          <div>
                            <v-row style="align-items: center; text-align: center; justify-content: center;">
                              <v-col cols="12" sm="4">
                                <v-card color="#03242d">
                                  <h1  id="datotension" >
                                    {{tension}}
                                  </h1>
                                </v-card>
                              </v-col>
                              <v-col cols="12" sm="4">
                                <v-progress-circular
                                  class="my-4"
                                  :rotate="90"
                                  :size="200"
                                  :width="35"
                                  :value="tensiometro"
                            
                                  :color="color"
                                >
                                <strong>{{tensiometro}} %</strong>
                                  
                                </v-progress-circular>
                              </v-col>
                            </v-row> 
                          </div>
                        </v-card>
                      </div>
                      <div>
                        <v-slider
                        
                        class="ml-3 mt-15"
                        v-model="valorslider"
                        label="Rango mayor"
                        thumb-color="black"
                        thumb-label="always"
                        max="4095"
                        :min="0">
                        
                        </v-slider>
                        {{enviartensionmayor}}
                        <v-slider
                          class="ml-3 mt-5"
                          v-model="tension"
                          label="Datos sensor"
                          :thumb-color="colorcab"
                          thumb-label="always"
                          max="4095"
                          :min="0"
                          :color="colorcab"
                          :track-color="colorcab"
                        ></v-slider>
                        <v-slider
                        class="ml-3 mt-4"
                          v-model="valorslidermenor"
                          label="Rango menor"
                          thumb-color="green"
                          thumb-label="always"
                          max="4095"
                          :min="0"
                        ></v-slider>
                      </div>
                      <div class="d-flex" style="flex-direction:column ;">
                        <v-card elevation="0" width="210" class="my-0 py-0 mx-auto d-flex">
                          <v-card-subtitle 
                        
                          class="my-0 py-0 mx-auto">Límites</v-card-subtitle>
                        </v-card>
                        <v-card elevation="0" width="210" class="my-0 py-0 mx-auto d-flex">
                          <v-card class="my-0 py-0 mx-auto" width="200"
                          v-bind:style="valorslidermenor>=valorslider?'background-color:red':'' "
                          >
                          
                          <v-card-title class="my-0 py-0" 
                            style="justify-content: center"                 
                            >{{valorslidermenor}}-{{valorslider}} 
                          </v-card-title>
          
                          </v-card>
                          <v-icon
                          v-if="valorslidermenor>=valorslider"
                          class="ml-2" color="error">mdi-alert-circle-outline</v-icon>
                        </v-card>

                      </div>                  
                    </v-card>              
                  </v-col>
                  <v-col cols="12" sm="4">
                    <v-card elevation="0" style="text-align:center;" > 
                            <v-avatar
                            class="mt-7 mb-15"
                              v-if="estado_boton"
                              color="primary"
                              size="40"
                              style="-moz-box-shadow: 0px 2px 25px 24px #1976d2;
                              box-shadow:  0px 2px 25px 24px #1976d2;"
                            >
                              <v-avatar
                                color="white"
                                size="10"
                                style="-moz-box-shadow: 0px 0px 7px 7px #fff;
                                box-shadow:  0px 0px 7px 7px #fff;"
                              >
    
                              </v-avatar>
                            </v-avatar>
                            {{estado_motor}}
                              <!--v-img

                              class="ma-auto rotate"
                              
                                src="https://icones.pro/wp-content/uploads/2022/02/services-parametres-et-icone-d-engrenage-orange.png"
                              ></v-img-->
                              <div 
                              class="mt-15 ma-auto contenedorimg"
                              >
                              <img
        
                              v-bind:style="estado_motor==1?'animation: rotation 1s infinite linear;':''"
                              src="https://icones.pro/wp-content/uploads/2022/02/services-parametres-et-icone-d-engrenage-orange.png" alt="">
                              </div>
                              
                    </v-card>
                  </v-col>
                </v-row>          
              </v-card>
             </template>
          </v-container>
     
    </v-main>
  </v-container>
</template>

<script>
import mqtt from 'mqtt'
  export default {
    name: 'HelloWorld',
    data(){
      return{
        client: mqtt.connect("ws://broker.emqx.io:8083/mqtt"),
        estado_boton: 0, 
        temperatura:23,
        humedad:37,
        limite:'',
        tension:2486,
        valorslider:0,
        valorslidermenor:0,
        estado_motor:0,
        colorcab:'red',

        publish: {
          topic: 'oriolport/02',
          qos: 0,
          payload: '0',
        },
    }
      
    },mounted(){

    /*db.collection("tension").doc('Cp1EZMP8tdMUpG0AZBTZ')
    .onSnapshot((doc) => {
        var dato=doc.data();

           this.valorslider=dato.valor2;
           this.valorslidermenor=dato.valor1;

    });*/
    //this.audio();

       this.client.on('connect', ()=>{
      console.log('conectado')
      this.client.subscribe('oriolport/01',(err)=> {
        if (!err) {
          this.client.publish('oriolport/02', '0')
        }
      })
    })
      this.client.on('message',(topic, message)=>{
        // message is Buffer
        if(topic=='oriolport/01'){
          //console.log(message.toString())
          let js=message.toString();
          let tension=JSON.parse(js);
          console.log(tension)
          this.tension=tension.tension;
        }
      })
  },   
  computed:{
    color() {
      if (this.tension < 100) return '#90CAF9'
      if (this.tension < 250) return '#42A5F5'
      if (this.tension < 500) return '#1565C0'
      if (this.tension < 750) return '#26C6DA'
      if (this.tension < 1000) return '#00ACC1'
      if (this.tension < 1250) return '#00838F'
      if (this.tension < 1500) return '#80DEEA'
      if (this.tension < 1750) return '#1DE9B6'
      if (this.tension < 2000) return '#66BB6A'
      if (this.tension < 2100) return '#69F0AE'
      if (this.tension < 2250) return '#00E676'
      if (this.tension < 2500) return '#76FF03'
      if (this.tension < 2750) return '#B2FF59'
      if (this.tension < 3000) return '#F4FF81'
      if (this.tension < 3100) return '#EEFF41'
      if (this.tension < 3250) return '#FFEE58'
      if (this.tension < 3500) return '#FBC02D'
      if (this.tension < 3750) return '#FF8F00'
      if (this.tension < 4000) return '#FF7043'
      if (this.tension < 4095) return '#673AB7'
      return 'red'
    },

     enviartensionmayor:function(){
      if(this.valorslider>this.valorslidermenor){
          var limite='{"tipo":"tension","tension1" :'+this.valorslider+',"tension2":'+this.valorslidermenor+'}';
          //this.connection.send(limite);
          console.log(limite)
      }
      return ''
      

    }
    ,tensiometro(){
       this.calcular()
       return (this.tension*100/4995).toFixed(1);
    }
    
  },      
  methods:{
    calcular(){
      if(this.tension<this.valorslider && this.tension>this.valorslidermenor){
        this.estado_motor=1
        this.colorcab='amber darken-1'
      }else{
        this.estado_motor=0
        this.colorcab='pink accent-3'
      }
    },

    guardar(){
      /*
      db.collection("tension").doc("Cp1EZMP8tdMUpG0AZBTZ").set({
        valor1:this.valorslidermenor,
        valor2:this.valorslider,
      })
      .then(() => {
          console.log("Datos guardados");
      })
      .catch((error) => {
          console.error("Error writing document: ", error);
      });*/
    },
    recibir(event){
      var datosSensor = event.data;
      var data = JSON.parse(datosSensor);
      this.tension=data.tension;
      //this.temperatura = data.temp;
      //this.humedad = data.hum;
    },
     
    botonOn(){
      this.estado_boton ='1'; 
      console.log("Led is ON")
      this.enviarDato()
     // this.audio.play();
    },

    botonOff(){
      //this.audio.pause(); 
      //this.audio.currentTime = 3;
      this.estado_boton = '0';
      console.log("Led is OFF")
      this.enviarDato()
    },
    enviarDato(){
      this.publish.payload=this.estado_boton;
      const { topic, qos, payload } = this.publish;
      this.client.publish(topic, payload, qos, error => {
        if (error) {
          console.log('Publish error', error)
        }
      })

    },
    enviarlimite(){
      if(!isNaN(this.limite)){ 
        console.log(this.limite);
        var limite1='{"tipo":"limite","limite1" :'+this.limite+'}';
        console.log(limite1)
      }

    },
    prendermotor(){
      console.log('hola')
      this.estado_motor=1;
      var motor='{"tipo":"motor","motor" :'+1+'}';
      console.log(motor)
      //this.connection.send(motor);
    },
    apagarmotor(){
      this.estado_motor=0;
      this.valorslider=1;
      this.valorslidermenor=0;
      
      var motor='{"tipo":"motor","motor" :'+0+'}';
      console.log(motor)
    },


  }
  }
</script>
<style >
.led_on{
    border: 1px solid;
    width: 30px;
    height: 30px;
    border-radius: 50%;
  }

.titulo{
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: blue;
}
#datotension{
  font-family: 'DS-Digital', sans-serif;
  font-size: 55px;
  color: #75dfd8;
}
.contenedorimg{
  width: 100%;
}
.contenedorimg img{
  width: 80%;
}
.rotate {
  animation: rotation .5s infinite linear;
}
@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}



/*
.cuadro{
  top: 10px;
  left: 15%;
  background: pink;
  height: 160px;
  width: 85%;
  position: absolute;
}

.caja-cuadro{
  position: relative;
}*/
</style>

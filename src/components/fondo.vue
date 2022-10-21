<template>
    <div class="fondo">
    <v-card class="transparent" elevation="0">
        <v-card-title style="color:#bdc2c5; font-size:30px" >
          <v-icon style="color:#bdc2c5; font-size:30px" dark class="mr-2" @click="dialog=true">mdi-view-dashboard</v-icon> Control de Sensores
          <v-menu 
            transition="slide-x-transition"
            bottom
            right
            v-model="dialog"
            
            :close-on-content-click="false"
            
            >
            <v-list width="350" style="background:#031119" dark>
                <v-list-item>
                    <v-list-item-title>
                        Controles del sistema
                    </v-list-item-title>
                </v-list-item>
       
                <v-list-item
      
                >
                <v-list-item-title>
                     <v-icon>mdi-cog-off</v-icon>Sistema  
                     
                </v-list-item-title>
                <v-switch v-model="sistema" @click="estado_sistema()" class="ml-4" color="#03fda1"></v-switch>
                </v-list-item>

                <v-list-item
                >
                <v-list-item-title>
                     <v-icon>mdi-led-on</v-icon> Led
                </v-list-item-title>
                    <v-switch v-model="led" @click="prenderled()" class="ml-4"  color="#01c4ff"></v-switch>
                </v-list-item>

                <v-list-item
                >
                <v-list-item-title>
                     <v-icon>mdi-led-on</v-icon> Motor
                </v-list-item-title>
                    <v-switch v-model="estado_motor" @click="prender_motor()" class="ml-4"  color="#01c4ff"></v-switch>
                </v-list-item>

            </v-list>
            </v-menu> 
        </v-card-title>
    </v-card>
        <v-card class="mx-3 mt-2 transparent" elevation="0" >
            <v-row>
                <v-col cols="12" sm="4">
                    <v-card class="transparent card1" >
                        <v-card-title class="colorletra" style="position:relative; width:100%;">
                            Temperatura Ambiente
                            <v-icon dark style="position:absolute; right:0;  top:5px" size="70" color="#f9f82dfc">mdi-thermometer</v-icon>
                        </v-card-title>
                        <v-card elevation="0" class="transparent d-flex" height="240" >
                            <strong style="color:#e9701afc" class="color_numero">{{temp}}°C</strong>   
                        </v-card>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="4">
                    <v-card class="transparent card1"  >
                        <v-card-title class="colorletra" style="position:relative; width:100%;">
                            Humedad de suelo
                            <v-icon dark style="position:absolute; right:0;  top:5px" size="70" color="#2df997fc">
                                mdi-water-outline
                            </v-icon>
                        </v-card-title>
                           <v-card elevation="0" class="transparent d-flex" height="240">
                                 <v-progress-circular :value="hume" size="220" class="mx-auto mb-4" color="rgba(38, 233, 139, 0.625) ">
                                    <strong color="rgba(38, 233, 139, 0.625)" style="font-size:55px">{{hume}} %</strong>
                                </v-progress-circular>
                            </v-card>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="4">
                    <v-card class="transparent card1"  >
                        <v-card-title class="colorletra" style="position:relative; width:100%;">
                            Lluvia
                        </v-card-title>
                           <v-card elevation="0" class="transparent d-flex" height="240">   
                                <div class="mx-auto">
                                    <v-icon dark class="my-auto mx-auto" size="150" color="#1cc3c3">
                                        mdi-cloud-outline
                                    </v-icon >
                                    <div v-if="lluvia" style="text-align: center;">
                                        <v-icon  dark  size="50" color="#1cc3c3" style="animation: nieve 2s ease-in-out infinite;">
                                            mdi-water
                                        </v-icon>
                                        <v-icon  dark  size="50" class="mt-7"  color="#1cc3c3" style="animation: nieve 2s ease-in-out infinite;">
                                            mdi-water
                                        </v-icon>
                                        <v-icon  dark  size="50" color="#1cc3c3" style="animation: nieve 2s ease-in-out infinite;">
                                            mdi-water
                                        </v-icon>
                                    </div>
                                </div> 
                               
                                
                            </v-card>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="5">
                    <v-card class="mb-3 card2" >
                        <v-card-title class="colorletra" style="position:relative; width:100%;">
                            Hora  {{hor}}
                            <v-icon dark style="position:absolute; right:0;  top:5px" size="70" color="#ef476f">mdi-clock</v-icon>
                        </v-card-title>
                        <v-card elevation="0" class="transparent d-flex" height="140" >
                            <div class="container">
                                <div class="reloj">
                                    {{hora}}:{{minutos}} {{hora>=12?'PM':'AM'}}
                                </div>
                            </div>   
                        </v-card>
                    </v-card>
                    <v-card class=" card3" >
                        <v-card-title class="colorletra" style="position:relative; width:100%;">
                            Estación
                        </v-card-title>
                        <v-card elevation="0" class="transparent d-flex" height="140" >
                            <div class="estacion">
                                <div >
                                    <div v-if="estacion==1" class="verano" style="animation: rotation 3.5s infinite linear;">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#fff76e"> mdi-white-balance-sunny</v-icon>  
                                    </div>
                                    <div v-else-if="estacion==2" class="invierno" style="animation: nieve 2s ease-in-out infinite;">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#118ab2">mdi-snowflake</v-icon>
                                    </div> 
                                    <div v-else-if="estacion==4" class="primavera" style="">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#ef476f">mdi-flower</v-icon>
                                        
                                    </div>
                                    <div v-else-if="estacion==3" class="otoño" style="animation: otoño 3s ease-in-out infinite;">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#e9701afc">mdi-seed</v-icon>
                                        
                                    </div>
                                   
                                </div>
                             
                            </div>  
                                <div class="date">
                                    <div class="mb-3">
                                    <v-chip color="#fff76e" small @click="cambiarestacion(1)">
                                        Verano
                                    </v-chip>
                                    <v-chip class="ml-1" color="#118ab2" small @click="cambiarestacion(2)" >Invierno</v-chip>
                                    <v-chip class="ml-1" color="#e9701afc" small @click="cambiarestacion(3)" >Otoño</v-chip>
                                    <v-chip class="ml-1" color="#ef476f" small @click="cambiarestacion(4)" >Primavera</v-chip>
                                    </div>
                                    {{nombreest}}
                                </div>
                        </v-card>
                    </v-card>
                </v-col>
                
                <v-col cols="1" >
                      <strong style="color:#fff;">Resumen de datos</strong> 
                      <v-alert
                      class="mt-4"
                        border="bottom"
                        color="#e9701afc"
                        dense
                        loading
                       style="color:#fff !important;"
                      >
                        Temperatura {{temp}}°C
                        <v-progress-linear
                        v-if="sistema"
                        indeterminate
                        color="white"
                        ></v-progress-linear>
                      </v-alert>
                      <v-alert
                        border="bottom"
                        color="#2df997fc"
                        dense
                        style="color:#fff !important;"
                      >
                       Humedad {{humedad}}%
                        <v-progress-linear
                        v-if="sistema"
                        indeterminate
                        color="white"
                        ></v-progress-linear>
                      </v-alert>
                      <v-alert
                        border="bottom"
                        color="#1cc3c3"
                        dense
                     style="color:#fff !important;"
                      >
                       {{lluvia?'Con':'Sin'}} lluvia
                        <v-progress-linear
                        v-if="sistema"
                        indeterminate
                        color="white"
                        ></v-progress-linear>
                      </v-alert>
                      <v-alert
                        border="bottom"
                        color="#ef476f"
                        dense
                        style="color:#fff !important;"
                      >
                         Hora <br>
                        {{hora}}:{{minutos}} pm
                         <v-progress-linear
                         v-if="sistema"
                        indeterminate
                        color="white"
                        ></v-progress-linear>
                      </v-alert>
                      <v-alert
                        border="bottom"
                        color="purple"
                        dense
                        style="color:#fff !important;"
                      >
                        {{nombreest}}
                         <v-progress-linear
                        v-if="sistema"
                        indeterminate
                        color="white"
                        ></v-progress-linear>
                      </v-alert>
                </v-col>

                <v-col cols="12" sm="6">
                    <v-card class="transparent">
                        <div 
                        class="ma-auto contenedorimg"
                        >
                        <img
                        v-bind:style="estado_motor==1?'animation: rotation 1s infinite linear;':''"
                        src="https://icones.pro/wp-content/uploads/2022/02/services-parametres-et-icone-d-engrenage-orange.png" alt="">
                        </div>
                    </v-card>
                </v-col>
               
            </v-row>
        </v-card>
    </div>
</template>

<script>
import mqtt from 'mqtt';
export default {
    name:'fondo',
    data(){
        return{
            dialog:false,
            sistema:true,
            led:0,
            client: mqtt.connect("ws://broker.emqx.io:8083/mqtt"),
            humedad:0,
            temperatura:0,
            lluvia:0,
            hora: 12,
            minutos: 35,
            segundos: 59,
            dia: 20,
            mes: "Octubre",
            verano: 1,
            estacion:1,
            nombreest:'Verano',
            estado_motor:0,
            tiempo:0,
           // hume:0,
            count:0,
           datos:{
            humedad:0,
            temperatura:0,
            hora:0,
            estacion:0,
            lluvia:0,

           }
        }
    },computed:{
        hume(){
            return Math.round((((1300-this.humedad)/1400)*100))
        },
        temp(){
            return Math.round(this.temperatura/100)
        },
        hor(){
            this.obtenerhora();
            return '';
        },
    },    
    mounted(){

        let brains = document.createElement('script')
        brains.setAttribute('src', '//unpkg.com/brain.js')
        document.head.appendChild(brains)

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
                if(topic=='oriolport/01' && this.sistema){
                    //console.log(message.toString())
                    let js=message.toString();
                    let cadena=JSON.parse(js);
                    //console.log(cadena)
                    this.humedad=cadena.hume;
                    this.lluvia=cadena.lluvia?0:1;
                    this.temperatura=cadena.temp;
                    this.tiempo=cadena.hora;
                   // this.estado_motor=1;
                   // console.log(this.lluvia)
                    if(this.count==4){
                        this.count=0;
                        this.ejecutor();
                    }
                    this.count++;
                }else{
                    this.humedad=0;
                    this.lluvia=0;
                    this.temperatura=0;
                    this.estado_motor=0;
                }

                //setInterval(this.ejecutor(),5000)
            })
  

    },methods:{
        prenderled(){
            let l=this.led?'1':'0';
              this.client.publish('oriolport/02', 'e'+l)
        },
        estado_sistema(){
            let s=this.sistema?'1':'0';
            if(s=='0'){
              this.client.publish('oriolport/02', 'm0')
            }
        },
     
        obtenerhora(){
            this.hora=Math.round(this.tiempo/170);
            //let hor=Math.round(this.tiempo/24);
            let rangmin=Math.round(this.tiempo%170);
            let min=Math.round((rangmin*60)/170)
            this.minutos=min;
        }
        ,
        prender_motor(){
            let s=this.estado_motor?'1':'0';
            this.client.publish('oriolport/02', 'm'+s)
        },
        cambiarestacion(es){
            switch(es){
                case 1:
                    this.nombreest='Verano';
                    this.estacion=1;
                    break;
                case 2:
                    this.nombreest='Invierno';
                    this.estacion=2;
                    break;
                case 3:
                    this.nombreest='Otoño';
                    this.estacion=3;
                    break;
                case 4:
                    this.nombreest='Primavera';
                    this.estacion=4;
                    break;
                default :
                    break;
            }
        },
        ejecutor(){
                this.datos.humedad=Math.round((((1300-this.humedad)/1400)*100));
                this.datos.temperatura= Math.round(this.temperatura/100);
                this.datos.hora=Math.round(this.tiempo/170);
                this.datos.estacion=this.estacion;
                this.datos.lluvia=this.lluvia;
                console.log(this.datos);
                const net=new brain.NeuralNetwork();
                return net;
            
        }
    }

}
</script>

<style >
@font-face {
  font-family: 'Open Sans';
  font-style: normal;
  font-weight: 300;
  src: local('Open Sans Light'), local('OpenSans-Light'), url(https://fonts.gstatic.com/s/opensans/v13/DXI1ORHCpsQm3Vp6mXoaTXhCUOGz7vYGh680lGh-uXM.woff) format('woff');
}
.fondo{
    background: #030e16;
    height: 100%;
    font-family: 'Open Sans';
    font-weight: 700;
}

.transparent{
    background-attachment: transparent !important;
    
}
.card1 {
        box-shadow: 0px 3px 3px -2px rgb(26 153 148 / 20%), 0px 3px 4px 0px rgb(12 96 48 / 14%), 0px 1px 8px 0px rgb(6 167 89 / 12%) !important;
        background: linear-gradient(to top, #030e16, #0b2f37);
}

.colorletra{
    color: #717b82;
    font-weight: 500;
    font-size: 25px
}
#circulotemp{
    margin: auto;
    background-color: transparent !important;
    height: 190px;
    width: 190px;
    border-radius: 50%;
    border:2px solid rgba(87, 225, 158, 0.474);
    margin-bottom: 10px;
    display: flex;
}
.color_numero{
    margin: auto;
    font-size: 85px;
}

.container{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-flow: wrap;

}

.reloj{
  display: flex;
  font-size: 70px;
  color: white;
  font-family: "Open Sans";
}

.date{
    display: flex;
    font-size: 25px;
    flex-direction: column;
    color: white;
    font-family: "Open Sans";
}

.estacion{
    display: flex;
    justify-content: center;
    align-content: center;
    width: 60%;
}
.card2{
    background-color: #00243c !important;
    /*box-shadow: 0px 3px 3px -2px rgb(26 153 148 / 20%), 0px 3px 4px 0px rgb(12 96 48 / 14%), 0px 1px 8px 0px rgb(6 167 89 / 12%) !important;*/
}

.card3{
     background-color:#13152c !important;
}

.contenedorimg{
     text-align: center !important;
}

.contenedorimg img{
  max-height: 50%;
  max-width: 70%;
 
}
.rotate {
  animation: rotation 1s infinite linear;
}
@keyframes rotation {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(359deg);
  }
}

@keyframes otoño{
    
    0%{
        transform: translateX(70px) ;
    }
    25%{
        transform: translateX(70px);
    }
    50%{
        transform: translateX(-70px) rotate(90deg);
    }
    75%{
        transform: translateX(-70px) rotate(90deg);
    }
    100%{
        transform: translateX(70px);
    }
   
    
}

@keyframes nieve{
    50%{
        transform: translateY(-30px);
    }100%{
        transform: translateY(0px);
    }
}
</style>
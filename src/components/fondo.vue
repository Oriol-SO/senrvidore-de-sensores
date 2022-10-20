<template>
    <div class="fondo">
    <v-card class="transparent" elevation="0">
        <v-card-title style="color:#bdc2c5; font-size:30px" >
          <v-icon style="color:#bdc2c5; font-size:30px" dark class="mr-2" >mdi-view-dashboard</v-icon> Control de Sensores 
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
                            <strong style="color:#e9701afc" class="color_numero">{{temperatura}}°C</strong>   
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
                                 <v-progress-circular :value="humedad" size="220" class="mx-auto mb-4" color="rgba(38, 233, 139, 0.625) ">
                                    <strong color="rgba(38, 233, 139, 0.625)" style="font-size:55px">{{humedad}} %</strong>
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
                            Hora
                            <v-icon dark style="position:absolute; right:0;  top:5px" size="70" color="#ef476f">mdi-clock</v-icon>
                        </v-card-title>
                        <v-card elevation="0" class="transparent d-flex" height="140" >
                            <div class="container">
                                <div class="reloj">
                                    {{hora}}:{{minutos}} PM
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
                                    <div v-else-if="estacion==3" class="primavera" style="">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#ef476f">mdi-flower</v-icon>
                                        
                                    </div>
                                    <div v-else-if="estacion==4" class="otoño" style="animation: otoño 3.5s ease-in-out infinite;">
                                        <v-icon dark style="right:0;  top:5px" size="130" color="#e9701afc">mdi-seed</v-icon>
                                        
                                    </div>
                                   
                                </div>
                             
                            </div>  
                                <div class="date">
                                    {{dia}} de  {{mes}} <br>
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
                        Temperatura {{temperatura}}°C
                        <v-progress-linear
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
                       Con lluvia
                        <v-progress-linear
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
                         Hora
                        {{hora}}:{{minutos}} pm
                         <v-progress-linear
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
                        Verano
                         <v-progress-linear
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
export default {
    name:'fondo',
    data(){
        return{
            humedad:75,
            temperatura:35,
            lluvia:1,
            hora: 12,
            minutos: 35,
            segundos: 59,
            dia: 20,
            mes: "Octubre",
            verano: 1,
            estacion:4,
            nombreest:'Verano',
            estado_motor:1,
        }
    },

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
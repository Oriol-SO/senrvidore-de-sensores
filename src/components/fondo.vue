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
                            <strong style="color:#f9ba2dfc" class="color_numero">24 °C</strong>   
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
                                 <v-progress-circular :value="100" size="220" class="mx-auto mb-4" color="rgba(38, 233, 139, 0.625) ">
                                    <strong color="rgba(38, 233, 139, 0.625)" style="font-size:55px">24 %</strong>
                                </v-progress-circular>
                            </v-card>
                    </v-card>
                </v-col>
                <v-col cols="12" sm="4">

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
    height: 100vh;
    font-family: 'Open Sans';
}

.transparent{
    background-attachment: transparent !important;
    
}
.card1 {
        box-shadow: 0px 3px 3px -2px rgb(26 153 148 / 20%), 0px 3px 4px 0px rgb(12 96 48 / 14%), 0px 1px 8px 0px rgb(6 167 89 / 12%) !important;
        /* fallback for old browsers */
        background: linear-gradient(to top, #030e16, #0b2f37); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}

.colorletra{
    color: #717b82;
    font-weight: 700;
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
</style>
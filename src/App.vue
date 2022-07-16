<template>
   
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
      
    >
    

      <v-tabs
        centered
        class="ml-n9"
        color="grey darken-1"
        
      >
        <v-tab
          v-for="link in links"
          :key="link"
          :to="link.path"
          style="color:#d96459;"
         
        >
        
          {{ link.text }} 
        </v-tab>
      </v-tabs>

     
    </v-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        
        <v-row>
         
            <!--<v-sheet
              rounded="lg"
              min-height="268"
            > 
            <p id="citat">Briga o ljepoti, trebali biste započeti sa srcem i dušom, inače vam nikakva šminka neće pomoći. (Coco Chanel)</p>

            </v-sheet>-->
         
          

          <v-col
            cols="12"
 
            
          >
            <v-sheet id="prikaz"
            
              rounded="lg"
              style="border-radius:30px;"
              
            >
              <router-view></router-view>
            </v-sheet>
          </v-col>

          
           
          
          
            <!--<v-sheet
              rounded="lg"
              min-height="268"
            >
                
             <p id="citat"> Kad ste tužni, razočarani u ljubav, - šminkajte se, najbolja frizura - i napadnite. (Coco Chanel).</p>
              <br>


            </v-sheet>-->
         
        </v-row>
      </v-container>
     
      
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ( {

    


      links: [
       {
         text: 'Naslovnica',
         path:'/'
        
       },
       {
         text: 'Kontakt',
         path:'/Kontakt'
       },
       
       {
         text: 'Termini',
         path:'/Last'
       },
       {
         text: 'ponude',
         path:'/ponude'
       }
      ],
    }),
    
  }
</script>
<style scoped>
#citat{font-family: 'Lucida Handwritng',cursive;
color:#d96459;
  
}
main {
  background-image: url("./assets/pozadina.jpg");
  background-position: center;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background-size: cover;
}

#prikaz {
  border-radius:30px;
  padding: 100px;
}



</style>
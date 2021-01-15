<template>
  <v-container>
    <v-col>
      <v-row class="justify-center">
        <v-card color="#CBD5E0" style="height:50% width:50%;">
          <v-col>
            <v-row> </v-row>
          </v-col>
          <v-col>
            <v-row class="justify-center">
              <v-card-title primary-title>
                <h3 class="#2C3E50--text">
                   <h3>Function1</h3>
                </h3>
              </v-card-title>
            </v-row>
          </v-col>

          <v-col>
            <v-row class="justify-center">
             <h4>{{ product_Total }}</h4>
            </v-row>
          </v-col>
          
        </v-card>
      </v-row>
    </v-col>
  </v-container>
</template>

<script>
import json from "../exam-data.json";

export default {
  data: () => ({
    myJsons: json,
    product_Total:[],
    sumWeight:null
  }),

   mounted() {
      this.product = this.myJsons.filter((jsonData) => {
          if(jsonData.is_editable_price == false){
                return jsonData
          }
        })

    this.Find_main_product = this.product
    for (var i = 0; i < (this.Find_main_product.length); i++) {
      this.sumWeight = 0
      let PName = this.Find_main_product[i].name 
      this.Find_main_product[i].products.map(val =>{this.sumWeight += val.weight})
      this.product_Total.push({"name":PName ,"totalSubProductWeight": this.sumWeight})
    }
     console.log(this.product_Total);
        

  }
};
</script>

<style></style>

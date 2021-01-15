<template>
  <v-container>
    <v-col>
      <v-row class="justify-center">
        <v-card color="#CBD5E0" style="width:40%;">
          <v-col>
            <v-row> </v-row>
          </v-col>
          <v-col>
            <v-row class="justify-center">
              <v-card-title primary-title>
                <h3 class="#2C3E50--text">
                  เขียน function ตรวจหา max อันดับที่ 2 ของ array
                </h3>
                  <v-row>
                    <v-col cols="12">
                      <v-row justify="center">
                        <v-subheader><h2 class="#2C3E50--text mt-10">Input Number in Code</h2></v-subheader>
                      </v-row>
                    </v-col>
                  </v-row>
              </v-card-title>
            </v-row>
          </v-col>

          <v-col>
            <v-row class="justify-center">
             <h1>{{getMaxValueNumber2()}}</h1> 
            </v-row>
          </v-col>
          
        </v-card>
      </v-row>
    </v-col>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    arr:[]  //<= input number
  }),

  methods: {
    getMaxValueNumber2() {

      if (this.arr.length > 0) {
        if (this.arr.length == 1) {
            return this.arr[0];
        } else {
            if (this.arr.length == 2 && this.arr[0] == this.arr[1]) {
                return this.arr[0];
            } else {
                var arrSoerted = this.arr.sort((a, b) => {return b - a;})
                .reduce((prev, cur) => (prev.includes(cur) ? prev : prev.concat(cur)),[]);
                return arrSoerted[1];
            }
        }
      } else {
        return 'null';
      }
    },
  },
};
</script>

<style></style>

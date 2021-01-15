<template>
  <v-container>
    <v-col>
      <v-row class="justify-center">
        <v-card color="#CBD5E0" style="width:40%;">
          <v-col>
            <v-row> </v-row>
          </v-col>
          <v-col md="12">
            <v-row class="justify-center">
              <v-card-title primary-title>
                <h3 class="#2C3E50--text">
                  {{ rawdate }}
                </h3>
              </v-card-title>
            </v-row>
          </v-col>

          <v-col>
            <v-row class="justify-center">
              <h2>ให้แปลงรูปแบบวันที่กำหนดให้เป็น format ดังต่อไปนี้</h2>
            </v-row>
            <br/>
            <br/>
            <v-row class="justify-center">
              <h2>{{Dateformat(rawdate)}} </h2>
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
    rawdate: "2020-08-10T14:54:52+07:00",
  }),

  methods: {
    Dateformat: (rawdate) => {
          if (rawdate) {
                var days = new Date(rawdate).getDate();
                var month = new Date(rawdate).getMonth()+1;
                var years = new Date(rawdate).getFullYear();
                var hours = new Date(rawdate).getHours();
                var mins = new Date(rawdate).getMinutes();
                var secs = new Date(rawdate).getSeconds();
                return `${days}/${month}/${years} ${hours}:${mins}:${secs}`
                +"\n" +
                new Date(rawdate).toLocaleDateString('th-TH', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    // weekday: 'long',
                }) 
                + '\n // รูปแบบปฏิทินไทย ' +
                new Date(years, month, 0).getDate()
                +'\n // จำนวนวันในเดือนนี้ '+
                Math.floor((month + 2) / 3)
                +'\n // ไตรมาตรของเดือนนี้ '+
                Math.round((new Date(rawdate)).getTime() / 1000)
                + '\n // Unix timestamp'
                // +'\n'+ 
                // new Date(rawdate).toLocaleFormat('%d/%m/%Y');
            } else {
                return rawdate;
            }
    },
  },
};
</script>

<style></style>

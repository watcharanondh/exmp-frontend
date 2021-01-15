<template>
  <v-container>
    <v-col>
      <v-row class="justify-center">
        <v-card color="#CBD5E0" style="width:40%;">
          <v-col>
            <v-row class="justify-center">
              <v-card-title primary-title>
                <h3 class="#2C3E50--text mt-10">Text form and validation</h3>
              </v-card-title>
            </v-row>
          </v-col>
          <v-card-text>
            <form>
              <v-row justify="center">
                <v-col>
                  <!-- First Name -->
                  <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                        <v-subheader
                          ><h2 class="#2C3E50--text mt-10">
                            First Name
                          </h2></v-subheader
                        >
                      </v-row>
                    </v-col>
                    <v-col md="8">
                      <v-text-field
                        v-model="firstname"
                        :error-messages="firstnameErrors"
                        solo
                        placeholder="Please fill first name"
                        required
                        @input="$v.firstname.$touch()"
                        @blur="$v.firstname.$touch()"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                  <!-- Last Name -->
                  <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                        <v-subheader><h2 class="#2C3E50--text mt-10">Last Name</h2></v-subheader>
                      </v-row>
                    </v-col>
                  <v-col md="8">
                  <v-text-field
                    v-model="lastname"
                    placeholder = "Please fill last lastname"
                    :error-messages="lastnameErrors"
                    solo
                    required
                    @input="$v.lastname.$touch()"
                    @blur="$v.lastname.$touch()"
                  ></v-text-field>
                  </v-col>
                </v-row>
                 <!-- E-mail -->
                    <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                    <v-subheader><h2 class="#2C3E50--text mt-10">E-mail</h2></v-subheader>
                           </v-row>
                        </v-col>
                    <v-col md="8">
                      <v-text-field
                        v-model="email"
                        placeholder = "Please fill email"
                        :error-messages="emailErrors"
                        solo
                        required
                        @input="$v.email.$touch()"
                        @blur="$v.email.$touch()"
                      ></v-text-field>
                   </v-col>
                  </v-row>

                  <!-- Password -->
                      <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                        <v-subheader><h2 class="#2C3E50--text mt-10">Password</h2></v-subheader>
                      </v-row>
                    </v-col>
                    <v-col md="8">
                      <v-text-field
                        v-model="password"
                        placeholder = "Please fill password"
                        :error-messages="passwordErrors"
                        solo
                        @input="$v.password.$touch()"
                        @blur="$v.password.$touch()"
                        :append-icon="isShowPassword ? 'visibility' : 'visibility_off'"
                        @click:append="isShowPassword = !isShowPassword"
                        :type="isShowPassword ? 'text' : 'password'"
                      />
                    </v-col>
                  </v-row>
                  
                  
                  <!-- Verify Password -->
                        <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                        <v-subheader><h2 class="#2C3E50--text mt-10">Verify Password</h2></v-subheader>
                      </v-row>
                    </v-col>
                    <v-col md="8">
                      <v-text-field
                        v-model="verifyPassword"
                        placeholder = "Please fill verify password"
                        :error-messages="verifyPasswordErrors"
                        solo
                        @input="$v.verifyPassword.$touch()"
                        @blur="$v.verifyPassword.$touch()"
                        :append-icon="isShowPassword ? 'visibility' : 'visibility_off'"
                        @click:append="isShowPassword = !isShowPassword"
                        :type="isShowPassword ? 'text' : 'password'"
                      />
                    </v-col>
                  </v-row>

                  <!--Gender-->
                 <v-row>
                    <v-col cols="4">
                      <v-row justify="end">
                        <v-subheader><h2 class="#2C3E50--text mt-10">Gender</h2></v-subheader>
                      </v-row>
                    </v-col>
                    <v-col md="8">
                      <v-select
                        v-model="selectGender"
                        :items="items_Gender"
                        :error-messages="selectgenderErrors"
                        label="please select a Gender"
                        required
                        @change="$v.selectGender.$touch()"
                        @blur="$v.selectGender.$touch()"
                        return-object
                        single-line
                        filled
                        dense
                        solo
                        outlined
                        clearable
                      ></v-select>
                    </v-col>
                  </v-row>

                  <!--Submit-->
                  <v-row>
                    <v-col cols="4">
                    </v-col>
                    <v-col md="8">
                    <v-btn class="white--text" color="success" @click="submit" >Submit</v-btn>    
                     </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </form>

            <div v-if="showInput== true">
              <h2>Result:</h2>
              <h3>First Name: {{ firstname }}</h3>
              <h3>Last Name: {{ lastname }}</h3>
              <h3>E-mail : {{ email }}</h3>
              <h3>Gender :{{ selectGender }}</h3>
            </div>
          </v-card-text>
        </v-card>
      </v-row>
    </v-col>
  </v-container>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required, maxLength, minLength, email , sameAs } from "vuelidate/lib/validators";

export default {
  data: () => ({
    isShowPassword: false,
    showInput:false,

    firstname: "",
    lastname: "",
    password:'',
    verifyPassword:'',
    email: '',

    selectGender: null,  
    items_Gender:['Male','Female'],

  }),

  mixins: [validationMixin],

  validations: {
    firstname: { required, maxLength: maxLength(15) },
    lastname: { required, maxLength: maxLength(15) },
    password: { required, minLength: minLength(6) },
    verifyPassword : { required, minLength: minLength(8) ,sameAsPassword: sameAs('password') },
    email: { required, email },
    selectGender : { required },
  },

  computed: {
    firstnameErrors() {
      const errors = [];
      if (!this.$v.firstname.$dirty) return errors;
      !this.$v.firstname.maxLength && errors.push("firstname must be at most 10 characters long");
      !this.$v.firstname.required && errors.push("firstname is required.");
      return errors;
    },
    lastnameErrors() {
      const errors = [];
      if (!this.$v.lastname.$dirty) return errors;
      !this.$v.lastname.maxLength && errors.push("lastname must be at most 10 characters long");
      !this.$v.lastname.required && errors.push("lastname is required.");
      return errors;
    },
    passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.minLength && errors.push('Password must have at least 6 letters.')
        !this.$v.password.required && errors.push('Password is required.')
        return errors
      },
    verifyPasswordErrors () {
        const errors = []
        if (!this.$v.verifyPassword.$dirty) return errors
        !this.$v.verifyPassword.sameAsPassword && errors.push('Passwords must be identical.')
        !this.$v.verifyPassword.required && errors.push('Verify password is required.')
        return errors
      },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    },
     selectgenderErrors () {
        const errors = []
        if (!this.$v.selectGender.$dirty) return errors
        !this.$v.selectGender.required && errors.push('Gender is required')
        return errors
      },
  },

  methods: {
    submit() {
      console.log(this.$v.$invalid);
      this.$v.$touch();
      if(this.$v.$invalid == false){
          this.showInput = true
       }
      }
      
  },
};
</script>

<style></style>

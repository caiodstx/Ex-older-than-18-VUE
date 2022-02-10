<template>
  <v-container>
    <v-card elevation="24">
      <v-card-text>
        <form>
          <v-text-field
            v-model="name"
            :error-messages="nameErrors"
            :counter="10"
            label="Name"
            required
            @input="$v.name.$touch()"
            @blur="$v.name.$touch()"
          ></v-text-field>
          <v-text-field
            v-model="age"
            :error-messages="ageErrors"
            label="Your Age"
            required
            @input="$v.age.$touch()"
            @blur="$v.age.$touch()"
          ></v-text-field>
          <v-card-actions id="btns">
            <v-btn rounded outlined text @click="submit"> submit </v-btn>
            <v-btn rounded outlined text @click="clear"> clear </v-btn>
          </v-card-actions>
        </form>
      </v-card-text>
      <v-alert id="drive-alert">{{ message }}</v-alert>
    </v-card>
  </v-container>
</template>


<script>
import { validationMixin } from "vuelidate";
import { required, maxLength } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],

  name: "AgeCheck",

  validations: {
    name: { required, maxLength: maxLength(10) },
    age: { required },
  },

  data: () => ({
    name: "",
    age: "",
    message: "",
  }),

  computed: {
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 10 characters long");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    ageErrors() {
      const errors = [];
      if (!this.$v.age.$dirty) return errors;
      !this.$v.age.required && errors.push("Age is required");
      return errors;
    },
  },

  methods: {
    submit() {
      let age = this.age;
      if (age >= 18) {
        this.message = "You can drive!";
      } else {
        this.message = "You can't drive :(";
      }
      this.$v.$touch();
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.age = "";
    },
  },
};
</script>

<style lang="scss">
#btns {
  font-family: poppins, sans-serif;
}

#dirve-alert {
  display: flex;
  justify-content: center;
}
</style>
<template>
  <v-container class="d-flex justify-content-center">
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
      !this.$v.age.age && errors.push("Must be valid age");
      !this.$v.age.required && errors.push("Age is required");
      return errors;
    },
  },

  methods: {
    submit() {
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
</style>
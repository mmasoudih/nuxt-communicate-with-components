<template>
  <div>
    <v-form v-model="valid" ref="form">
      <v-dialog v-model="openModal" persistent max-width="600px">
        <v-card>
          <v-card-title>
            <span class="headline">User Profile</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12">
                  <v-text-field
                    label="First Name"
                    required
                    :rules="nameRules"
                    :counter="10"
                    v-model="childState.firstName"
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="Last Name"
                    required
                    :rules="nameRules"
                    :counter="10"
                    v-model="childState.lastName"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="closeModal()">
              Close
            </v-btn>
            <v-btn color="blue darken-1" text @click="saveInput()">
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-form>
  </div>
</template>

<script>
export default {
  props: ["openModal","emptyField"],
  data() {
    return {
      valid: false,
      childState: {
        firstName: "",
        lastName: ""
      },
      nameRules: [v => !!v || "Name is required"]
    };
  },
  methods: {
    closeModal() {
      this.$emit("closeModal", false);
    },
    saveInput() {
      if (this.$refs.form.validate()) {
        this.$emit("saveItem", this.childState);
      }
    }
  },
  watch:{
    openModal(value){
      if(value){
        this.$refs.form.reset();
        this.childState.firstName = '';
        this.childState.lastName = '';

      }
    }
  }
};
</script>

<template>
  <v-container fill-height fluid>
    <v-card class="ma-auto pa-10" width="600" height="700">
      <v-container fluid fill-height class="d-flex align-start">
        <v-row>
          <v-col cols="12" class="mb-10 d-flex justify-center">
            <span class="display-1">CREAT YOUR ACCOUNT</span>
          </v-col>
          <v-col cols="12" class="px-10 pa-2">
            <v-text-field
              v-model="name"
              label="your name"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" class="px-10 pa-2">
            <v-text-field
              v-model="position"
              label="your position"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" class="px-10 pa-2">
            <v-text-field
              v-model="account"
              label="your account"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" class="px-10 pa-3">
            <v-text-field
              v-model="password"
              label="your password"
              :rules="[rules.required]"
              :type="show ? 'text' : 'password'"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              class="pa-0"
              @click:append="show = !show"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" class="px-10 pa-3 pb-0">
            <v-text-field
              v-model="password_com"
              label="confirm your password"
              :rules="[rules.required]"
              :type="show1 ? 'text' : 'password'"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              class="pa-0"
              @click:append="show1 = !show1"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" sm="6" class="d-flex justify-start pl-10 pa-0">
            <v-btn depressed text tile :to="{ name: 'login1___en' }"
              >back to log in</v-btn
            >
          </v-col>
          <v-col
            cols="12"
            sm="6"
            class="d-flex {justify-end:this.$vuetify.breakpoint.smAndUp} pa-0"
          >
            <v-btn
              depressed
              text
              x-large
              tile
              block
              class="ma-auto"
              color="grey darken-1"
              @click="create_account()"
              >create</v-btn
            >
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    name: null,
    position: null,
    account: null,
    password: null,
    password_com: null,
    show: false,
    show1: false,
    rules: {
      required: (value) => !!value || 'Required.'
    }
  }),
  methods: {
    async create_account() {
      if (
        this.name &&
        this.position &&
        this.account &&
        this.password &&
        this.password_com
      ) {
        if (this.password === this.password_com) {
          const num = await this.$axios.$post('/api/account', {
            name: this.name,
            position: this.position,
            account: this.account,
            password: this.password
          })
          if (num === 0) {
            this.account = null
            alert('this account have been register !!')
          } else if (num === 1) {
            alert('register success !!')
            this.$router.push('/')
          }
        } else if (this.password !== this.password_com) {
          alert('your password isn`t the same plz refill it')
          this.password = null
          this.password_com = null
        }
      }
    }
  }
}
</script>

<style></style>

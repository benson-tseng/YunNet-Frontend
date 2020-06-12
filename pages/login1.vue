<template>
  <v-container fill-height fluid>
    <v-card class="ma-auto py-10" width="600" height="600" outlined>
      <v-container fluid fill-height class="d-flex align-start">
        <v-row class="d-flex justify-center">
          <v-col cols="12" class="mb-10 d-flex justify-center">
            <span style="font-size:40px">WELCOME !!</span>
          </v-col>
          <v-col cols="12" sm="8" class="py-1 px-5">
            <v-text-field
              v-model="account"
              label="account"
              outlined
              rounded
              clearable
              :rules="[rules.required]"
              class="pa-0"
            ></v-text-field>
          </v-col>
          <v-col cols="12" sm="8" class="py-1 px-5">
            <v-text-field
              v-model="password"
              label="password"
              outlined
              rounded
              :rules="[rules.required]"
              :type="show ? 'text' : 'password'"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              class="pa-0"
              @click:append="show = !show"
            ></v-text-field>
          </v-col>
          <v-col
            cols="12"
            sm="8"
            class="d-flex justify-start pl-4 pa-0 align-center mb-5"
          >
            <v-btn
              :to="{ name: 'register___en' }"
              small
              depressed
              text
              color="black"
            >
              <span>haven't got an account yet?</span>
            </v-btn>
          </v-col>
          <v-col cols="12" class="px-5 pa-0 mt-5 d-flex justify-center">
            <v-btn outlined color="grey darken-2" x-large @click="sign_in()">
              sign in
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    alldata: {},
    ip: null,
    account: null,
    password: null,
    show: false,
    rules: {
      required: (value) => !!value || 'Required.'
    }
  }),
  methods: {
    async sign_in() {
      if (this.account && this.password) {
        const response = await this.$axios.$get('/api/account', {
          params: { account: this.account, password: this.password }
        })
        if (response === 11) {
          alert('登入成功')
          this.$store.commit('infoes/set_v', {
            text: 'account',
            value: this.account
          })
          this.$router.push('/info')
        } else if (response === 0) {
          alert('無此帳號')
          this.password = null
          this.account = null
        } else if (response === 10) {
          alert('密碼錯誤')
          this.password = null
        }
      } else {
        alert('fill the blank !!')
      }
    },
    async fetchSomething() {
      const ip = await this.$axios.$get('/api/account')
      // eslint-disable-next-line no-console
      console.log(ip)
    },
    test() {
      document.cookie = 'user=pass'
    }
  }
}
</script>

<style></style>

<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="groupLogin"
        label="Email address:"
        label-for="inputLogin"
        description="Please use e-mail!"
      >
        <b-form-input
          id="inputLogin"
          v-model="form.login"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="groupPass" label="Password:" label-for="inputPass">
        <b-form-input
          id="inputPass"
          v-model="form.passwd"
          type="password"
          placeholder="****"
          required
        ></b-form-input>
      </b-form-group>
      <b-container fluid>
        <b-row align-v="center">
            <b-col><b-button type="submit" variant="primary">Submit</b-button></b-col>
            <b-col><b-button type="reset" variant="danger">Reset</b-button></b-col>
        </b-row>
      </b-container>
    </b-form>
  </div>
</template>

<script>
  export default {
    data() { 
      return {
        addr: "/v1/user/login",
        ret: "",
        form: {
            login: '',
            passwd: '',
        },
        show: true,
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        this.getData()
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.login = ''
        this.form.passwd = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      async getData() {
        const response = await axios
          .post(this.addr, this.form)
//          .then(response => (this.ret = response.data))
          .catch(error => {
            console.error("There was an error!", error);
          })
        console.log(response.data)
        this.ret = response.data
        if (this.ret.id != null) {
          this.$emit('loginOk', this.ret.id)
        } else {
          console.log("Login fail!")
        }
      }

    }
  }
</script>

<style>

</style>
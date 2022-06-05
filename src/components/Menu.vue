<template>
  <div>
      <nav>
        <b-navbar toggleable="lg" type="dark" variant="info">
            <router-link to="/">
                <b-navbar-brand href="#">
                    <img src="../assets/marvin.png" alt="Marvin" class="logoMenu">
                    Simple Org
                </b-navbar-brand>
            </router-link>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
<!--                <div v-for="menu in menus"> -->
                <div>
                    
<!--                    <b-nav-item href="#" disabled>Disabled</b-nav-item> -->
                </div>
            </b-navbar-nav>

            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <b-nav-form>
                <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
                <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
                </b-nav-form>

                <b-nav-item-dropdown text="Lang" right>
                <b-dropdown-item href="#">EN</b-dropdown-item>
                <b-dropdown-item href="#">ES</b-dropdown-item>
                <b-dropdown-item href="#">RU</b-dropdown-item>
                <b-dropdown-item href="#">FA</b-dropdown-item>
                </b-nav-item-dropdown>

                <b-nav-item-dropdown right>
                <!-- Using 'button-content' slot -->
                <template #button-content>
                    <em>User</em>
                </template>
                <b-dropdown-item href="#" @click="$bvModal.show('modalLogin')">Login</b-dropdown-item>
                <b-dropdown-item href="#">Profile</b-dropdown-item>
                <b-dropdown-item href="#">Sign Out</b-dropdown-item>
                </b-nav-item-dropdown>
            </b-navbar-nav>
            </b-collapse>
        </b-navbar>
        </nav>
        <div>
            <b-modal id="modalLogin" ref="modalLogin" title="Login" hide-footer>
                <Login @loginOk="(id) => loadUser(id)"/>
            </b-modal>
        </div>
    </div>
    
</template>

<script>
import Login from '@/components/Login.vue'

export default {
    data(){
        return{
            menus: [
                {label: "Login", disabled: false, command: "'$bvModal.show('modalLogin')'"},
                {label: "Logoff", disabled: true, command: ""},
            ]
        }
    
    },
    components: {
        Login,
    },
    methods: {
        loadUser(id) {
            this.$refs['modalLogin'].hide()
            console.log("User id : " + id)
        }
    },
}
</script>

<style>
.logoMenu{
    height: 25px;
}
</style>
<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>ASSEMBLY</span>
        <span class="font-weight-light">GENERATOR</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="#"
        target="_blank"
      >
        <v-icon left>group_add</v-icon>
        <span class="mr-2">SING UP</span>
      </v-btn>
      <v-btn
        flat
        href="#"
        target="_blank"
      >
        <v-icon>persona</v-icon>
        <span class="mr-2">LOGIN</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <conversor/>
    </v-content>
  </v-app>
</template>

<script>
import conversor from './components/Conversor'

export default {
  name: 'App',
  components: {
    conversor
  },
  data () {
    return {
      //
    }
  }
}
</script>

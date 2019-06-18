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
        href="https://github.com/JulianGarzon22/AssemblyVuejs"
        target="_blank"
      >
        <span class="mr-2">GITHUB</span>
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

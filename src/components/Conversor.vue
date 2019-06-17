<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex md6>
        <v-textarea solo name="input-7-4" label="Copia y pega de tu tabla" v-model="table"></v-textarea>
      </v-flex>
      <v-flex md3>
        <v-hover>
          <v-card
            slot-scope="{ hover }"
            :class="`elevation-${hover ? 12 : 2}`"
            class="mx-auto"
            width="250"
          >
            <v-card-title>
              <div>
                <span class="headline">C++ Codes</span>
                <div class="d-flex">{{cppcodes}}</div>
              </div>
              <v-spacer></v-spacer>
              <v-btn icon class="mr-0">
                <v-icon>mdi-chevron-right</v-icon>
              </v-btn>
            </v-card-title>
          </v-card>
        </v-hover>
      </v-flex>
      <v-flex md3>
        <v-hover>
          <v-card
            slot-scope="{ hover }"
            :class="`elevation-${hover ? 12 : 2}`"
            class="mx-auto"
            width="250"
          >
            <v-card-title>
              <div>
                <span class="headline">Xilinx Codes</span>
                <div class="d-flex">{{vhdlcodes}}</div>
              </div>
              <v-spacer></v-spacer>
              <v-btn icon class="mr-0">
                <v-icon>mdi-chevron-right</v-icon>
              </v-btn>
            </v-card-title>
          </v-card>
        </v-hover>
      </v-flex>
    </v-layout>
    <v-btn color="info" target="_blank" @click.prevent="compile()">
      <span class="mr-2">COMPILAR</span>
    </v-btn>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    table: '',
    cppcodes: [],
    vhdlcodes: [],
  }),
  methods: {
    compile: function() {
      var splitlines = [];
      var rows = [];
      var lines = this.table.split("\n");
      for (var i = 0; i < lines.length; i++) {
        splitlines[i] = lines[i].split(" ");
        if(splitlines[splitlines[i].length()] =!0) {
          rows[i].operands = splitlines[splitlines.length()]
        } else {
          rows[i].operands = null;
        }
        var n = splitlines[i].length() - 1;
        if(splitlines[n] == ""){
          n = n-1;
        } else {
          rows[i].mnemo = splitlines[i]
        }
      }
      console.log(columns);
    }
  }
};
</script>

<style>
</style>

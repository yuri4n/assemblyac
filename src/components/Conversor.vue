<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex md6>
        <v-textarea solo name="input-7-4" label="Copia y pega de tu tabla" v-model="table"></v-textarea>
        <v-alert v-model="erroralert" type="error">Tienes un error en las instrucciones, revisa y vuelve a intentarlo</v-alert>
        <v-btn color="info" target="_blank" @click.prevent="compile()">
          <span class="mr-2">COMPILAR</span>
        </v-btn>
      </v-flex>
      <v-flex md3>
        <v-card>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">C++ Codes</h3>
              <div v-for="code in cppcodes" :key="code.id">{{code}}</div>
            </div>
          </v-card-title>
        </v-card>
      </v-flex>
      <v-flex md3>
        <v-card>
          <v-card-title primary-title>
            <div>
              <h3 class="headline mb-0">VHDL Codes</h3>
              <div v-for="codev in vhdlcodes" :key="codev.id">{{codev}}</div>
            </div>
          </v-card-title>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    isa: [
      "load",
      "store",
      "add",
      "sub",
      "input",
      "output",
      "jpos",
      "jneg",
      "jz",
      "jnz",
      "jmp",
      "halt"
    ],
    table: "",
    cppcodes: [],
    vhdlcodes: [],
    rows: [],
    dataarray: [],
    n: 0,
    erroralert: false
  }),
  methods: {
    compile: function() {
      this.cppcodes = [];
      this.vhdlcodes = [];
      var splitlines = [];
      var cppisa = [];
      var cppoperand = [];
      var lines = this.table.split("\n");

      for (let i = 0; i < lines.length; i++) {
        let z = i - 1;
        splitlines[i] = lines[i].split("\t");
        this.rows[i] = {
          section: splitlines[i][0],
          label: splitlines[i][1]
            ? splitlines[i][1].toLowerCase()
            : splitlines[i][1],
          mnemo: splitlines[i][2]
            ? splitlines[i][2].toLowerCase()
            : splitlines[i][2],
          operands: splitlines[i][3]
            ? splitlines[i][3].toLowerCase()
            : splitlines[i][3],
          hexindex: z.toString(16)
        };
      }

      for (let i = 0; i < this.rows.length; i++) {
        if (!this.rows[i].mnemo) {
          cppisa[i] = "0";
        } else {
          if (this.isa.indexOf(this.rows[i].mnemo) == -1) {
            this.erroralert = true;
          } else {
            cppisa[i] = this.isa.indexOf(this.rows[i].mnemo).toString(16);
          }
        }
      }

      this.n = this.rows
        .map(function(e) {
          return e.section;
        })
        .indexOf(".data");

      let x = 0;
      for (let j = this.n + 1; j < this.rows.length; j++) {
        this.dataarray[x] = {
          label: this.rows[j].label,
          hexindex: x.toString(16)
        };
        x++;
      }

      for (let i = 0; i < this.rows.length; i++) {
        if (this.rows[i].operands) {
          let codeoperand = this.rows.find(
            z => z.label == this.rows[i].operands
          );
          let dataoperand = this.dataarray.find(
            z => z.label == this.rows[i].operands
          );
          if (codeoperand && dataoperand) {
            if (dataoperand.hexindex.length == 1) {
              cppoperand[i] = "0" + dataoperand.hexindex;
            } else {
              cppoperand[i] = dataoperand.hexindex;
            }
          } else if (codeoperand && !dataoperand) {
            if (codeoperand.hexindex.length == 1) {
              cppoperand[i] = "0" + codeoperand.hexindex;
            } else {
              cppoperand[i] = codeoperand.hexindex;
            }
          } else {
            cppoperand[i] = "00";
          }
        } else {
          cppoperand[i] = "00";
        }

        if (this.rows[i].mnemo) {
          this.cppcodes.push(
            "0x" + cppisa[i].toUpperCase() + cppoperand[i].toUpperCase() + ","
          );
        }

        if (this.rows[i].mnemo) {
          this.vhdlcodes.push(
            'x"' +
              cppisa[i].toUpperCase() +
              cppoperand[i].toUpperCase() +
              '"' +
              ","
          );
        }
      }
    }
  }
};
</script>

<style>
</style>

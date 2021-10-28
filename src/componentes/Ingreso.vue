<template>

  <section class="src-componentes-ingreso">
    <div class="jumbotron">
      <h2>Ingreso de Gastos</h2>
      <hr>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input 
          type="text"
          id="nombre" 
          v-model="formData.nombre" 
          required
          :minlength="nombreMinLength"
          :maxlength="nombreMaxLength"
          name="nombre" 
          autocomplete="off" 
          class="form-control"
          no-espacios
          />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
               No se permiten espacios intermedios en este campo.
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres
            </div>
            <div v-show="formData.nombre && formData.nombre.length == nombreMaxLength" class="alert alert-danger mt-1">
              Este campo debe poseer como máximo {{ nombreMaxLength }} caracteres
            </div>
          </field-messages>
        </validate>
        <br>

        <!-- Campo descripcion -->
        <validate tag="div">
          <label for="nombre">Descripcion</label>
          <input 
          type="text"
          id="nombre" 
          v-model="formData.descripcion" 
          required
          :minlength="nombreMinLength"
          no-espacioss
          name="descripcion" 
          autocomplete="off" 
          class="form-control"
          
          />
    
          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
               No se permiten espacios intermedios en este campo.
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres
            </div>
            
          </field-messages>
        </validate>
        <br>

        <!-- Campo importe -->
        <validate tag="div">
          <label for="importe">Importe</label>
          <input type="number" id="importe" v-model.number="formData.importe" required name="importe" autocomplete="off" class="form-control" />
    
          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br>

       
        
        
       

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>
      
       <validate tag="div">
          <label for="pago">Presupuesto</label>
          <input type="number" id="pago" v-model.number="formData.pago" required name="pago" autocomplete="off" class="form-control" />
    
          <field-messages name="pago" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          </field-messages>
        </validate>
        <br> 


      <!-- Tabla para representar los datos ingresados -->
      <h2>Detalle de Gastos</h2>
      <br>

      <!-- <pre>{{ gastos }}</pre> -->

      <div v-if="gastos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Descripcion</th>
            <th>Importe</th>
            <th>Fecha</th>
          </tr>
          <!--  -->
          <tr v-for="(gasto,index) in gastos" :key="index" :style="{color: analizarSaldo(gasto).color }">
            <td>{{ gasto.nombre }}</td>
            <td>{{ gasto.descripcion }}</td>
            <td>{{ '$'+gasto.importe }}</td>
            <td>{{ gasto.fecha }}</td>
            <!-- <td>{{ analizarSaldo(gasto).valor }}</td> -->
          </tr>
          <tr>
            <th>Gasto total</th>
          </tr>
          <tr v-for="(gasto,i) in gastos" :key="i" :style="{color: analizarSaldo(gasto).color }">
            
            <td>{{ acumularGasto(gasto).valor }}</td>

          </tr>
        </table>
      </div>

      <h3 v-else class="alert alert-info">No hay gastos ingresados</h3>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-ingreso',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        gastos : [],
        nombreMinLength : 3,
        nombreMaxLength : 15,
        dniMax: 8,
        edadMin : 18,
        edadMax : 120,
        total: 0       
        
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          descripcion: null,
          pago: null,
          importe:null
          
        }
      },
      enviar() {
        let gasto = {...this.formData}
        gasto.fecha = new Date().toLocaleString()

        console.log(gasto)
        this.gastos.push(gasto)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      analizarSaldo(gasto) {

        let dif = gasto.pago - gasto.deuda
        let color = '#080'
        if(dif > 0) color = '#00F'
        if(dif < 0) color = '#F00'
        return {
          valor : dif,
          color
        }
      },
      acumularGasto(gasto){
        
        //let tot = this.total + gasto.importe
        this.total = this.total + gasto.importe
        //tot = tot + gasto.importe 
        
        /* let color = 'green'
        if(total > 1000 && total < 5000) color = '#FF00FF'
        if(total > 5000) color = 'orange' */
        return {
          valor : this.total
          
        }
      }
    },

    computed: {
    }
}


</script>

<style scoped lang="css">
  .src-componentes-ingreso {

  }

  .jumbotron {
    background-color: lightyellow;
    color: brown;
  }

  hr {
    background-color: #eee;
  }

  pre {
    color: white;
  }
</style>

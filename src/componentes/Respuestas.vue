<template>

  <section class="src-componentes-respuestas">
    <div class="jumbotron">
      <h2>Respuestas</h2>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr>
            <td>1</td>
            <td>b, d</td>
          </tr>
          <tr>
            <td>2</td>
            <td>c</td>
          </tr>
          <tr>
            <td>3</td>
            <td>b, e</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-respuestas {

  }

  .jumbotron {
    background-color: green;
    color: white;
  }
</style>

<template>
  <div>
    <b-modal :id="'modal-' + id" size="lg" title="Detalles de nave">
	<div class="modal-content">
	<div class="modal-body">
	<div v-if="loading" class="loading">
	<h2>Cargando...</h2>
	</div>
		<div v-if="nave" class="content">
      <table class="table table-hover table-dark">
      <tbody>
		<tr>
			<th>Nombre</th>
			<td>{{nave.name}}</td>
		</tr>
		<tr>
			<th>Modelo</th>
			<td>{{nave.model}}</td>
		</tr>
		<tr>
			<th>Fabricante</th>
			<td>{{nave.manufacturer}}</td>
		</tr>
		<tr>
			<th>Coste (créditos)</th>
			<td>{{nave.cost_in_credits}}</td>
		</tr>
		<tr>
			<th>Velocidad máxima en la atmósfera</th>
			<td>{{nave.max_atmosphering_speed}}</td>
		</tr>
		<tr>
			<th>Tripulación</th>
			<td>{{nave.crew}}</td>
		</tr>
		<tr>
			<th>Pasajeros</th>
			<td>{{nave.passengers}}</td>
		</tr>
		<tr>
			<th>Capacidad</th>
			<td>{{nave.cargo_capacity}}</td>
		</tr>
		<tr>
			<th>Consumibles</th>
			<td>{{nave.consumables}}</td>
		</tr>
		<tr>
			<th>Ratio de hipersalto</th>
			<td>{{nave.hyperdrive_rating}}</td>
		</tr>
		<tr>
			<th>MGLT</th>
			<td>{{nave.MGLT}}</td>
		</tr>
		<tr>
			<th>Clase de nave</th>
			<td>{{nave.starship_class}}</td>
		</tr>
		</tbody>
		</table>
    </div>
</div>
</div>
</b-modal>
<b-button v-b-modal="'modal-' + id">Ver detalles</b-button>

  </div>
</template>

<script>
export default {
  name: 'ModalDetalles',
  data () {
    return {
      loading: false,
      nave: null,
      error: null
    }
  },
  props: {
    urlnave : String,
	id: Number
  },
  mounted () {
	this.error = this.nave = null
    this.loading = true
	fetch(this.urlnave).then(res => res.json()).then(finalResult => {
		this.nave = finalResult;
		this.loading = false
	}).catch(error => this.error = error.toString())
	
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

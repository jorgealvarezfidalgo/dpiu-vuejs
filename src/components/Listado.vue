<template>
  <div class="listado row d-flex justify-content-center">
    <div v-if="loading" class="loading">
      <h2>Cargando...</h2>
    </div>

    <div v-if="error" class="error">
      {{ error }}
    </div>

    <div v-if="info" class="content w-75">
      <p>Se han encontrado {{ info.count }} resultados.</p>
		<table class="table table-hover table-dark">
		<thead>		
		<tr>
		<th>Nombre</th>
		<th>Modelo</th>
		<th>Opciones</th>
		</tr>
		</thead>
		<tbody>
		<tr v-for="(nave, index) in info.results" :key="nave.name">
			<td>{{nave.name}}</td>
			<td>{{nave.model}}</td>
			<td>
			<ModalDetalles :urlnave="nave.url" :id="index"/>
			</td>
		</tr>
		</tbody>
		</table>
		<ul>
			<li v-for="index in paginas" :key="index">
			<a v-if="param == ('?page=' + index)" :href="'?page=' + index"><strong>{{ index }}</strong></a>
			<a v-else-if="param == '' && index == 1" :href="'?page=' + index"><strong>{{ index }}</strong></a>
			<a v-else :href="'?page=' + index">{{ index }}</a>
			</li>
		</ul>
    </div>
	
  </div>
  
</template>

<script>
import ModalDetalles from './ModalDetalles.vue'
export default {
  name: 'Listado',
  components: {
	ModalDetalles
  },
  data () {
    return {
      loading: false,
      info: null,
      error: null,
      paginas: 1,
      param: ""
    }
  },
  mounted () {
	this.error = this.info = null
    this.loading = true
	let uri = window.location.href.split('?');
	if(uri[1]) {
		this.param = "?" + uri[1];
	}
	fetch('https://swapi.dev/api/starships/' + this.param).then(res => res.json()).then(finalResult => {
		this.info = finalResult;
		this.paginas = Math.ceil(this.info.count / 10);
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

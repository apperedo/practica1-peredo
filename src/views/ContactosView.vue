<template>
    <div>
      <h1>{{ titulo }}</h1>
      <div class="filtro">
        Filtro: <input type="search" v-model="textoBuscar">
      </div>
      <table>
        <thead>
            <tr>
                <th>id</th>
                <th>Name</th>
                <th>Email</th>
                <th>Address</th>
                <th>Phone</th>
                <th>Country</th>
                <th>City</th>
                <th></th>
            </tr>
            <tr>
                <th><input type="text" v-model="contactoNuevoObj.id"></th>
                <th><input type="text" v-model="contactoNuevoObj.name"></th>
                <th><input type="text" v-model="contactoNuevoObj.email"></th>
                <th><input type="text" v-model="contactoNuevoObj.address"></th>
                <th><input type="text" v-model="contactoNuevoObj.phone"></th>
                <th><input type="text" v-model="contactoNuevoObj.country"></th>
                <th><input type="text" v-model="contactoNuevoObj.city"></th>
                <th><button @click="guardarNuevo()">Nuevo</button></th>
            </tr>
            <tr v-if="indexParaEditar !== null">
                <th><input type="text" v-model="contactoEditarObj.id"></th>
                <th><input type="text" v-model="contactoEditarObj.name"></th>
                <th><input type="text" v-model="contactoEditarObj.email"></th>
                <th><input type="text" v-model="contactoEditarObj.address"></th>
                <th><input type="text" v-model="contactoEditarObj.phone"></th>
                <th><input type="text" v-model="contactoEditarObj.country"></th>
                <th><input type="text" v-model="contactoEditarObj.city"></th>
                <th><button @click="guardarEdicion()">Guardar</button></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(contacto, index) in listaContactosComputada":key="contactos.id">
                <td>{{ contacto.id }}</td>
                <td>{{ contacto.name }}</td>
                <td>{{ contacto.email }}</td>
                <td>{{ contacto.address }}</td>
                <td>{{ contacto.phone }}</td>
                <td>{{ contacto.country }}</td>
                <td>{{ contacto.city }}</td>
                <td>
                    <button @click="eliminarContacto(index)">Eliminar</button>
                    <button @click="editarContacto(contacto, index)">Editar</button>
                </td>
            </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    name: 'MiComponente',
    data() {
      return {
        titulo: 'Agenda de Contactos',
        textoBuscar: '',
        contactoNuevoObj:{
            id: "",
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        contactoEditarObj:{
            id: "",
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        indexParaEditar:null,
        contactos: [
            {id: 1, name: "Evelyn Carter", email: "evelyn.carter@example.com", address: "123 Maple Street", phone: "(202) 555-0185", country: "US", city: "Washington, DC"},
            {id: 2, name: "Liam Johnson", email: "liam.johnson@example.com", address: "456 Oak Avenue", phone: "(415) 555-2123", country: "US", city: "San Francisco, CA"},
            {id: 3, name: "Olivia Smith", email: "olivia.smith@example.com", address: "789 Pine Road", phone: "(305) 555-3647", country: "US", city: "Miami, FL"},
            {id: 4, name: "Ethan Davis", email: "ethan.davis@example.com", address: "321 Birch Lane", phone: "(312) 555-4890", country: "US", city: "Chicago, IL"},
            {id: 5, name: "Sophia Brown", email: "sophia.brown@example.com", address: "654 Cedar Drive", phone: "(617) 555-7305", country: "US", city: "Boston, MA"},
            {id: 6, name: "Noah Wilson", email: "noah.wilson@example.com", address: "987 Elm Street", phone: "(416) 555-2398", country: "CA", city: "Toronto, ON"},
            {id: 7, name: "Isabella Taylor", email: "isabella.taylor@example.com", address: "135 Spruce Street", phone: "(604) 555-7164", country: "CA", city: "Vancouver, BC"},
            {id: 8, name: "Aiden Moore", email: "aiden.moore@example.com", address: "246 Willow Avenue", phone: "(514) 555-9273", country: "CA", city: "Montreal, QC"},
            {id: 9, name: "Mia Anderson", email: "mia.anderson@example.com", address: "369 Maple Drive", phone: "(780) 555-5432", country: "CA", city: "Edmonton, AB"},
            {id: 10, name: "James Lee", email: "james.lee@example.com", address: "582 Pine Crescent", phone: "(403) 555-6789", country: "CA", city: "Calgary, AB"}
        ]
      }
    },
    components: {
      // Registro de componentes que se utilizaran.
    },
    methods: {
      // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
      guardarNuevo(){
        this.contactos.push(Object.assign({},this.contactoNuevoObj));
      }, 
      eliminarContacto(index){
        this.contactos.splice(index, 1);
      },
      guardarEdicion(){
        this.contactos[this.indexParaEditar] = Object.assign({}, this.contactoEditarObj);
        this.indexParaEditar = null;
      },
      editarContacto(contacto, index){
        this.indexParaEditar = index;
        this.contactoEditarObj = Object.assign({}, contacto);
      }
    },
    computed: {
      // propiedades computadas que dependen de otras propiedades reactivas
      listaContactosComputada(){
        return this.contactos.filter(item => item.name.toLowerCase().includes(this.textoBuscar.toLowerCase())||item.email.toLowerCase().includes(this.textoBuscar.toLowerCase()))
      }
    },
    props: {
      // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
  }
  </script>
  
  <style scope>
  h1 {
    color: #42b983;
  }
  th, td {
    border: 1px solid #ddd;
    padding: 10px;
  }
  th {
    background-color: #f2f2f2;
    text-align: left;
  }
  </style>
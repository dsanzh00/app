<template>
    <div class="row">
        <div class="col">
            <table class="table table-bordered table-hover">
                <thead>
                    <th >
                        <td>
                            <button class="btn btn-secondary" v-on:click="addDoc()">
                                <span class="material-icons-two-tone">
                                    add
                                    </span>
                            </button>
                        </td>
                        <td>
                            <button class="btn btn-secondary" onclick="location.href='http://localhost:8080/'">
                                <span class="material-icons-two-tone">
                                    logout
                                    </span>
                            </button>
                        </td>
                        <td>
                            <button class="btn btn-secondary" onclick="location.href='http://localhost:8080/menu'">
                                <span class="material-icons-two-tone">
                                    arrow_back
                                    </span>
                            </button>
                        </td>
                    </th>
                </thead>
            </table>
        </div>
    </div>
  <div class="row">
    <div class="col">
        <div class="table-responsive">
            <table class="table table-bordered table-hover">
                <thead><tr><th>#</th><th>Nombre</th><th>Estado</th><th>Categoría</th><th>Asignación</th><th>Acción</th></tr></thead>
                <tbody class="table-group-divider" id="Contenido">
                    <tr v-for="doc, i in documents" :key="doc.id">
                        <td>{{ (i+1) }}</td>
                        <td>{{ doc.data_file_name }}</td>
                        <td>{{ doc.status_data }}</td>
                        <td>{{ doc.category }}</td>
                        <td>{{ doc.assignee }}</td>
                        <td>
                            <button class="btn btn-danger" v-on:click="eliminar(i+1, doc.data_file_name)">
                                <span class="material-icons-two-tone">
                                    delete
                                    </span>
                            </button>

                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default{

    
    
    data(){
        return{ documents:null}
    },
    mounted(){
        this.getDocuments();
    },
    methods:{

        getDocuments(){
            axios.post('https://app.konfuzio.com/api/v3/auth/', new URLSearchParams({
            'username': 'dsanzh00@estudiantes.unileon.es',
            'password': 'tfg12345'}))
            .then(
                result => {
                    console.log(result.data);
                    console.log(result.data.token);
                    if(result.status === 200){
                        axios.get('https://app.konfuzio.com/api/v3/documents/', {
                            params: {
                                'limit': '80',
                                
                            },
                            headers: {
                                'accept': 'application/json',
                                'Authorization': 'Basic ZHNhbnpoMDBAZXN0dWRpYW50ZXMudW5pbGVvbi5lczp0ZmcxMjM0NQ=='
                            }
                            }).then(
                            response => {
                                console.log(response.data.results)
                                this.documents = response.data.results;
                            });
                    }
                }

                
            );

            
        },

        eliminar(id, nombre){
            confirmar(id, nombre);
        }, 

        addDoc(){
            
        }

    }
}
</script>


<template>
    <v-container>
        <v-row>
            <v-col class="mb-4">
                <h1 class="display-2 font-weight-bold-mb-3">Ingreso de Usuarios</h1>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <form v-on:submit.prevent="guardarUsuario()">
                    <v-text-field 
                        v-model="usuario.codigo"
                        label="Codigo"
                        outlined
                        required
                    >
                    </v-text-field>
                    <v-text-field 
                        v-model="usuario.user"
                        label="Usuario"
                        outlined
                        required
                    >
                    </v-text-field>
                    <v-text-field 
                        v-model="usuario.nombres"
                        label="Descripcion"
                        outlined
                        required
                    >
                    </v-text-field>
                    <v-text-field
                        v-model="usuario.clave"
                        :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                        :rules="[rules.required, rules.min]"
                        :type="show1 ? 'text' : 'password'"
                        name="input-10-1"
                        label="Clave"
                        hint="Minimo 8 caracteres"
                        counter
                        @click:append="show1 = !show1"
                    ></v-text-field>
                    <v-card-actions>
                        <v-btn to="/usuarios" color="blue-grey" class="mr-4">Cancelar</v-btn>
                        <v-btn type="submit" color="indigo" class="mr-4">Guardar</v-btn>
                    </v-card-actions>
                </form>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
let url = 'http://localhost:3000/user/'
import axios from 'axios';
export default {
    name:'CrearUsuario',
    data(){
        return{
            show1: false,
            rules: {
                required: value => !!value || 'Requerido.',
                min: v => v.length >= 8 || 'Minimo 8 caracteres',
            },
            usuario:{
                tipo_usuario_id:0,
                codigo:'',
                user:'',
                nombres:'',
                clave: ''
            }
        }
    },
    methods:{
        guardarUsuario(){
            let router=this.$router;
            let params = this.usuario;
            axios.post(url,params)
            .then(()=>{
                router.push('/usuarios');
            })
            .catch(error=>{
                console.log(error.response.data);
            })
        }
    }
}
</script>
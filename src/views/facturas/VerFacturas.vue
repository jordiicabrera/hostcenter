<template>
    <v-container>
        <v-row>
            <v-col class="mb-4">
                <h1 class="display-2 font-weight-bold-mb-3">Factura</h1>
            </v-col>
        </v-row>
        <v-row>
            <v-col>
                <form>
                    <v-text-field 
                        v-model="categoria.codigo"
                        label="Codigo"
                        outlined
                        readonly
                    >
                    </v-text-field>
                    <v-text-field 
                        v-model="categoria.descripcion"
                        label="Descripcion"
                        outlined
                        required
                    >
                    </v-text-field>
                    <v-card-actions>
                        <v-btn to="/facturas" color="blue-grey" class="mr-4">Cancelar</v-btn>
                        <!-- <v-btn type="submit" color="indigo" class="mr-4">Guardar</v-btn> -->
                    </v-card-actions>
                </form>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
let url = 'http://localhost:3000/categorias/'
import axios from 'axios';
export default {
    name:'VerFactura',
    mounted(){
        //OBTENGO TODOS LOS DATOS
        this.factura_id=this.$route.params.id
        //console.log(this.producto_id);
        axios.get(url+this.factura_id)
        .then(response=>{
            this.factura=response.data.factura[0]
        }).catch((error)=>{
            console.log("El error de la peticion"+error);
        });
    },
    data(){
        return{
            factura_id:null,
            factura:{
                persona_id:'',
                vendedor_id:'',
                fecha:new Date().toISOString().substr(0, 10),
                cantidad_total:0,
                total_iva:0,
                total_descuento:0,
                valor_total:0,
                detalle:[
                    {
                        factura_id:null,
                        producto_id:null,
                        descripcion:null,
                        cantidad:null,
                        precio_unitario:null,
                        subtotal:null,
                        valor_descuento:null,
                        valor_iva:null,
                        valor_total:null
                    }
                ]
            },
        }
    },
    methods:{
    }
}
</script>
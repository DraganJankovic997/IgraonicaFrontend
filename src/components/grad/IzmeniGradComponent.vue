<template>
    <div class="d-flex justify-content-center" style="height:100%">
        <div class="w-md-50">
            <div>
                <div class="header">
                    <h5 class="display-4 mb-5">Izmeni grad</h5>
                </div>
                <div class="body">
                    <div class="row mb-2">
                        <span class="col-md-6">Naziv grada</span>
                        <input class="col-md-6 form-control" type="text" v-model="grad.naziv">
                    </div>
                    <div class="row mb-2">
                        <span class="col-md-6">Postanski kod</span> 
                        <input class="col-md-6 form-control" type="number" v-model="grad.postanski_kod">
                    </div>
                </div>
                <div class="footer">
                    <button type="button" class="btn btn-success mr-5"  @click="izmeni">Sacuvaj</button>
                    <button type="button" class="btn btn-secondary ml-5" @click="odustani">Odustani</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import gradService from '../../services/grad.service';
import sviGradovi from '../../components/grad/SviGradoviComponent';
export default {
    data: function(){
        return{
            grad: {
                naziv: "",
                postanski_kod: ""
            }
        }
    },
    methods:{
        izmeni() {
            gradService.editGrad(this.grad, this.$route.params.id)
            .then((res) => {
                this.$toastr.s('Grad je izmenjen.', "Grad izmenjeno!");
                this.$router.go('/');
            })
            .catch((err) => {
                this.$toastr.e(err.message, "Greska");
            });
            this.$router.push('/gradovi');
            
        },
        odustani() {
            this.$router.go(-1);
        }
    },
    created() {
        gradService.getGradById(this.$route.params.id)
        .then((res) => {
            this.grad=res['data']
        })
        .catch((err) => {
            console.log(err);
        });
    }
}
</script>
<style>
</style>
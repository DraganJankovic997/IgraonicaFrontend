<template>
    <div class="d-flex justify-content-center" style="height:100%">
        <div class="w-md-50">
            <div>
                <div class="header">
                    <h5 class="display-4 mb-5">Izmeni popust</h5>
                </div>
                <div class="body">
                    <div class="row mb-2">
                        <span class="col-md-6">Oznaka popusta</span>
                        <input class="col-md-6 form-control" type="text" v-model="popust.oznaka_popust">
                    </div>
                    <div class="row mb-2">
                        <span class="col-md-6">Vrednost popusta</span>
                        <input class="col-md-6 form-control" type="number" v-model="popust.vrednost_popust">
                    </div>
                </div>
                <div class="footer">
                    <button type="button" class="btn btn-success mr-5" @click="izmeni">Izmeni</button>
                    <button type="button" class="btn btn-secondary ml-5" @click="odustani">Odustani</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import popustService from '../../services/popust.service'
export default {
    data: function(){
        return{
            popust: {
                oznaka_popust: "",
                vrednost_popust: ""
            }
        }
    },
    methods:{
        izmeni(){
            popustService.editPopust(this.popust, this.$route.params.id)
            .then((res) => {
                this.$toastr.s('Pice je izmenjeno.', "Pice izmenjeno!");
                this.$router.go('/');
            })
            .catch((err) => {
                this.$toastr.e(err.message, "Greska");
            });
            this.$router.push('/popusti');
        },
        odustani() {
            this.$router.go(-1);
        }
    },
    created() {
        popustService.getPopustById(this.$route.params.id)
        .then((res) => {
            this.popust=res['data']
        })
        .catch((err) => {
            console.log(err);
        });
    }
}
</script>
<style>

</style>
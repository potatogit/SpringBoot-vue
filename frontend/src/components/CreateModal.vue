<template>
    <el-dialog title="Create" :visible="isVisible" :close-on-click-modal="false" :show-close="false">
        <el-form :model="form" >
            <el-form-item label="username" :label-width="formLabelWidth">
                <el-input v-model="form.username"/>
            </el-form-item>
            <el-form-item label="email" :label-width="formLabelWidth">
                <el-input v-model="form.email"/>
            </el-form-item>
            <el-form-item label="phone" :label-width="formLabelWidth">
                <el-input v-model="form.phone"/>
            </el-form-item>
            <el-form-item label="gender" :label-width="formLabelWidth">
                <el-select v-model="form.sex">
                    <el-option label="male" value="male"/>
                    <el-option label="female" value="female"/>
                </el-select>
            </el-form-item>
            <el-form-item label="zone" :label-width="formLabelWidth">
                <el-input v-model="form.zone"/>
            </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
            <el-button :plain="true" type="danger" @click="hideModal">Cancel</el-button>
            <el-button :plain="true" @click="createUser(form)">Create</el-button>
        </div>
    </el-dialog>
</template>

<script>
    export default {
        data: function () {
            return {
                formLabelWidth: "120px"
            }
        },

        props: ['isVisible', 'form'],

        methods: {
            hideModal: function() {
                this.$emit('hide-modal');
            },
            checkFieldEmpty: function (form) {
                if(form.username&&form.email&&form.phone&&form.sex&&form.zone){
                    return false;
                }
                return true;
            },
            createUser: function (form) {
               console.log(form);
               if(!this.checkFieldEmpty(form)){
                   this.$axios.post('http://127.0.0.1:8000/api/persons/create', form)
                       .then(function(response){
                           console.log(response);
                       })
                       .catch(function(error){
                           console.log(error);
                       });
                   location.reload();
               }
            }

        }
    }
</script>
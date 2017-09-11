<template>
    <el-dialog title="Create" :visible="isVisible" :close-on-click-modal="false" :show-close="false">
        <el-form :model="form" >
            <el-form-item label="username" :label-width="formLabelWidth"/>
            <el-input v-model="form.username"/>
        </el-form>
        <div slot="footer" class="dialog-footer">
            <el-button :plain="true" type="danger" @click="hideModal">Cancel</el-button>
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
            }
        }
    }
</script>
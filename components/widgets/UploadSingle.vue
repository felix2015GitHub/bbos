<template>
<div class="upload-single">
    <el-upload
        class="avatar-uploader"
        action=""
        :show-file-list="false"
        :on-success="handleAvatarSuccess"
        :before-upload="beforeAvatarUpload">
        <img v-if="imageUrl" :src="imageUrl" class="avatar">
        <i v-else class="el-icon-plus avatar-uploader-icon"></i>
        <div slot="tip" class="el-upload__tip">只能上傳jpg/png文件，且不超過500kb</div>
    </el-upload>       
</div>
</template>
<script>
    export default {
        data() {
            return {
                imageUrl: ''
            }
        },
        methods: {
            handleAvatarSuccess(res, file) { 
                this.imageUrl = URL.createObjectURL(file.raw);
            },
            beforeAvatarUpload(file) { 
                const isJPG = file.type === 'image/jpeg';
                const isLt2M = file.size / 1024 / 1024 < 2;

                if (!isJPG) {
                this.$message.error('上传头像图片只能是 JPG 格式!');
                }
                if (!isLt2M) {
                this.$message.error('上传头像图片大小不能超过 2MB!');
                }
                return isJPG && isLt2M;
            }
        }
    }       
</script>

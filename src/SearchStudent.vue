

<template>
    <div>
        <form>
            <label for="txtTuKhoa">Từ khóa:</label>
            <!-- Binding giá trị từ khóa với input -->
            <input type="text" id="txtTuKhoa" placeholder="Từ khóa cần tìm" v-model="tuKhoa">
            <!-- Binding sự kiện click của button với phương thức timKiem của Vue -->
            <button type="button" id="button-search" v-on:click="timKiem">Tìm kiếm</button>
        </form>
    </div>
</template>
  
<script>
export default {
   
    name: "SearchStudent",
    data() {
        return {
            tuKhoa: "",
        };
    },
    methods: {
        timKiem: function () {
            this.$emit('searchStudent', this.tuKhoa);
        },
    },
};
</script>

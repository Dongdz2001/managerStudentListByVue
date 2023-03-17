
<template>
    <div id="table-student">
        <table>
            <thead>
                <tr>
                    <th></th>
                    <th>Mã SV</th>
                    <th>Tên sinh viên</th>
                    <th>Ngày sinh</th>
                    <th>Giới tính</th>
                    <th>Khoa</th>
                    <th> Chỉnh sửa </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(student, index) in students" :key="index">
                    <td><input type="checkbox" @click="checkBoxFuc(student)" :checked="student.flag"></td>
                    <td>{{ student.id }}</td>
                    <td>{{ student.name }}</td>
                    <td>{{ student.birthday }}</td>
                    <td>{{ student.gender }}</td>
                    <td>{{ student.faculty }}</td>
                    <td>
                        <button @click="editStudentTableINDelete(student)" id="button-edit">Sửa</button>
                        <button @click="deleteOneStudentINTable(student)" id="button-delete">Xóa</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>

export default {
    name: "TableStudent",
    data() {
        return {
            student: { id: '###', name: 'none', birthday: '01/01/2001', gender: 'Nam', faculty: 'none', flag: false },
            editStudentAA: null,
        }
    },
    props: {
        students: {
            type: Array,
            required: true,
        }
    },
    methods: {
      
        editStudentTableINDelete: function (student){
            this.editStudentAA = student;
            this.$emit('editStudentFunc', student);
        },
        checkBoxFuc: function (student) {
            student.flag = !student.flag;
        },
        editStudent: function (student) {
 

            this.$emit('editStudentFunc', student);
        },

     

        deleteOneStudentINTable: function (student) {
            this.$emit('deleteOneStudent', student);
        }
    }

}
</script>

<style></style>
 
  
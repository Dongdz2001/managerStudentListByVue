<template>
  <div id="input-student">
    <div class="form-group">
      <label for="id-student">ID:</label>
      <input type="text" class="form-control" id="id-student" v-model="idStudent">
    </div>
    <div class="form-group">
      <label for="name-student">Tên:</label>
      <input type="text" class="form-control" id="name-student" v-model="nameStudent">
    </div>
    <div class="form-group">
      <label for="date-student">Ngày sinh:</label>
      <input type="date" class="form-control" id="date-student" v-model="dateStudent">
    </div>
    <div class="form-group">
      <label for="gender">Giới tính:</label>
      <input type="radio" class="form-control" id="gender-male" name="gender" value="Nam" v-model="genderStudent">Nam
      <input type="radio" class="form-control" id="gender-female" name="gender" value="Nữ" v-model="genderStudent">Nữ
    </div>
    <div class="form-group">
      <label for="faculty-student">Khoa:</label>
      <select class="form-control" id="faculty-student" v-model="facultyStudent">
        <option value="">Chọn khoa</option>
        <option value="Công nghệ thông tin">Công nghệ thông tin</option>
        <option value="Khoa học máy tính">Khoa học máy tính</option>
        <option value="Điện tử viễn thông">Điện tử viễn thông</option>
        <option value="Trí tuệ nhân tạo">Trí tuệ nhân tạo</option>
        <option value="Khoa học dữ liệu">Khoa học dữ liệu</option>
        
      </select>
    </div>

    <button class="btn btn-primary" @click="addStudent">Thêm mới</button>
    <button class="btn btn-primary" @click="updateStudent">Cập nhật</button>
    <button class="btn btn-danger" @click="deleteStudent">Xóa</button>
  </div>
</template>
<script>
// import { EventBus } from './EventBus.js';
export default {
  data() {
    return {
      idStudent: '',
      nameStudent: '',
      dateStudent: '',
      genderStudent: '',
      facultyStudent: '',
      flagStuden: false,
      // editStudent: { id: '###', name: 'none', birthday: '01/01/2001', gender: 'Nam', faculty: 'none', flag: false },
    }
  },
  props:  ['editStudent'],

  methods: {
    addStudent() {
      if (!this.idStudent || !this.nameStudent || !this.dateStudent || !this.genderStudent || !this.facultyStudent) {
        alert("Bạn phải nhập đầy đủ thông tin sinh viên");
        return;
      }
      const newStudent = {
        id: this.idStudent,
        name: this.nameStudent,
        birthday: this._formatBirthday(this.dateStudent),
        gender: this.genderStudent,
        faculty: this.facultyStudent,
        flag: this.flagStuden,
      };
      // Do something with the new student object here (e.g. save to database)
      console.log('New student:', newStudent);
      this.$emit('addStudent', newStudent);
    },
    tranferDataStudent: function(student) {
      this.idStudent =  student.id;
      this.nameStudent = student.name;
      this.dateStudent =   this._formatBirthdayDefault(student.birthday);
      this.genderStudent = student.gender;
      this.facultyStudent = student.faculty;
      this.flagStuden = student.flag;
      // console.log("updated!!" , this.editStudent);
    },
    updateStudent: function(){
      const editStudenNew = {
        id: this.idStudent,
        name: this.nameStudent,
        birthday: this._formatBirthday(this.dateStudent),
        gender: this.genderStudent,
        faculty: this.facultyStudent,
        flag: this.flagStuden,
      };
      this.$emit('updateStudent', editStudenNew);
    },
    deleteStudent: function() {
      this.$emit('deleteAllStudentCheckBox');
    },
    _formatBirthday: function (dateStudent){
      let date = dateStudent.split('-');
      return `${date[2]}/${date[1]}/${date[0]}`;
    },
    _formatBirthdayDefault: function (dateStudent){
      let date = dateStudent.split('/');
      return `${date[2]}-${date[1]}-${date[0]}`;
    }
  },

}
</script>
<style src="@/css/InputStudent.css" ></style>
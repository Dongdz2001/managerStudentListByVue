<template>
  <h1>Danh sách sinh viên</h1>
  <SearchStudent @searchStudent="searchStudent" />
  <InputStudent  :editStudent="studentEditTable"  @addStudent="addStudentTable" @updateStudent="updateStudent" @deleteAllStudentCheckBox="deleteAllCheckBoxStudent"  ref="child" />  
  <TableStudent :students="students" @deleteOneStudent="deleteOneStudentINTable"    @editStudentFunc="editStudentTableINDelete"
    />
 
</template>

<script>
import SearchStudent from './SearchStudent.vue';
import TableStudent from "./TableStudent.vue";
import InputStudent from "./InputStudent.vue";

export default {
  name: 'App',
  components: {
    SearchStudent,
    TableStudent,
    InputStudent,
  },
  data() {
    return {
      students: [
        { id: '001', name: 'Nguyen Van A', birthday: '01/01/1990', gender: 'Nam', faculty: 'Công nghệ thông tin', flag: false },
        { id: '002', name: 'Tran Thi B', birthday: '02/02/1991', gender: 'Nữ', faculty: 'Trí tuệ nhân tạo', flag: false },
        { id: '003', name: 'Pham Van C', birthday: '03/03/1992', gender: 'Nam', faculty: 'Điện tử viễn thông', flag: false },
        { id: '004', name: 'Hoang Thi D', birthday: '04/04/1993', gender: 'Nữ', faculty: 'Khoa học dữ liệu', flag: false },
        { id: '005', name: 'Le Van E', birthday: '05/05/1994', gender: 'Nam', faculty: 'Khoa học máy tính', flag: false },
        { id: '006', name: 'Nguyen Thi F', birthday: '06/06/1995', gender: 'Nữ', faculty: 'Công nghệ thông tin', flag: false },
        { id: '007', name: 'Tran Van G', birthday: '07/07/1996', gender: 'Nam', faculty: 'Trí tuệ nhân tạo', flag: false },
        { id: '008', name: 'Pham Thi H', birthday: '08/08/1997', gender: 'Nữ', faculty: 'Điện tử viễn thông', flag: false },
        { id: '009', name: 'Hoang Van I', birthday: '09/09/1998', gender: 'Nam', faculty: 'Khoa học dữ liệu', flag: false },
        { id: '010', name: 'Le Thi K', birthday: '10/10/1999', gender: 'Nữ', faculty: 'Khoa học máy tính', flag: false },
        { id: '011', name: 'Nguyen Van L', birthday: '11/11/2000', gender: 'Nam', faculty: 'Công nghệ thông tin', flag: false },
        { id: '012', name: 'Tran Thi M', birthday: '12/12/2001', gender: 'Nữ', faculty: 'Trí tuệ nhân tạo', flag: false }
      ],
      tempStudents: [],
    }
  },
  methods: {
    addStudentTable: function (student) {
      const index = this.students.findIndex((s) => s.id === student.id);
      if(index === -1){
        this.students.unshift(student);
      }else{
        alert(`Id sinh viên: ${student.id} đã tồn tại!`);
      }
    
    },
    deleteOneStudentINTable: function (student) {
      this.students = this.students.filter((s) => s.id !== student.id);
      this.tempStudents =  this.students.slice();
      // console.log(`Đã xóa sinh viên ${student.name} có mã số ${student.id}`);
    },
    editStudentTableINDelete: function (student) {
       this.studentEditTable = student;
      this.$refs.child.tranferDataStudent(student);
    },
    updateStudent: function (student) {
      const index = this.students.findIndex((s) => s.id === student.id);
      if (index !== -1) {
        this.students = this.students.map((s, i) => {
          if (i === index) {
            return { ...s, ...student };
          }
          return s;
        });
      }
    },
    deleteAllCheckBoxStudent: function(){
      this.students = this.students.filter((s) => s.flag !== true);
      this.tempStudents =  this.students.slice();
    },
    searchStudent: function (tuKhoa) {
        console.log("Đã tìm kiếm từ khóa: " + tuKhoa);
        if (this.tempStudents.length < this.students.length) {
          this.tempStudents = this.students.slice();
        }
        if (tuKhoa === "") {
              console.log(`hiihii:  ${this.students.length}`);
              this.students = this.tempStudents;
              return;
        }
        this.students = this.students.filter((student) =>
            student.name.toLowerCase().includes(tuKhoa.toLowerCase())
        );
    },


  }
}
</script>


<style src="@/css/App.css"></style>
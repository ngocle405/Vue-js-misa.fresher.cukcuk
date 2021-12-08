
<template>
  <div id="app">
    <TheNavBar />
    <TheHeader />
    <TheContent />
   <!-- <div>
      <input style="left:50%" class="test" v-model="fullName" />
       <label class="test">{{convertUpperFullName}}</label>
   </div> -->
 
  </div>
</template>

<script>
import TheNavBar from "./components/layout/TheNavBar.vue";
import TheHeader from "./components/layout/TheHeader.vue";
import TheContent from "./components/layout/TheContent.vue";
export default {
  components: {
    TheNavBar,
    TheHeader,
    TheContent,
  },
  data() {
    return {
      SortNumber: 1,
      fullName:"ngọc dz",
      customer: [
        {
          customerCode: "nv00001",
          fullName: "Lê thanh Ngọc",
        },
      ],
    };
  },
  methods: {
    btnAddOnClick() {
      return "gọi sự kiện btnAddOnClick ";
    },
  },
  //không có tác dụng gì,k truy cập được vào data;
  beforeCreate() {
    console.log("1,beforeCreate ------");
  },
  created() {
    console.log("2.created -----");
    console.log(this.btnAddOnClick());
    document.getElementsByClassName("test"); //chưa đc render
  },
  beforeMount() {
    console.log("3.beforeMount -----");

 
  },
  //chỉ hiện thị duy nhất 1 lần,được render
  mounted() {
    console.log("4.mounted -----");

    console.log(this.btnAddOnClick());
    document.getElementsByClassName("test");
  },
  //nên dùng befofupdate vì lúc đầu dom chưa dc render lại
  beforeUpdate() {
  
    console.log("5.beforeUpdate -----");

    var el = document.getElementsByClassName("test")[0];
    var number = el.value;
    if (parseInt(number) > 2) {
      el.classList.add("border-red");
    } else {
      el.classList.remove("border-red");
    }
  },
  //chạy sau beforeupdate
  // updated() {
   
  //      console.log("6.bUpdate -----");

  //   var el = document.getElementsByClassName("test")[0];
  //   var number = el.value;
  //   if (parseInt(number) > 2) {
  //     el.classList.remove("border-red");
  //   } else {
  //     el.classList.add("border-red");
  //   }
  // },
  // beforeDestroy() {
  //   console.log("7.beforeDestroy -----");
  // },
  // destroyed() {
  //     console.log("8.destroyed -----");
  // },
  //theo dõi sự thay đổi của dữ liệu và thực thi hành động kèm theo.
  watch:{
      fullName:function(value){
         console.log(value);
         switch (value) {
           case 'dm':
             alert("k dc bậy");
             break;
         }
      }
  },
  // thay đổi dữ liệu bên trong
  computed: {
    convertUpperFullName(){
      return this.fullName.toUpperCase();
    }
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>


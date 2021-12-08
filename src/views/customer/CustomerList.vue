<template>
  <div class="m-content">
    <div class="m-content-title">
      <div class="m-title-left">Danh sách nhân viên</div>
      <div class="m-add-employee">
        <button id="btlAddData" @click="btnAddOnClick" class="m-btn-icon">
          <div class="m-icon-add"></div>
          Thêm nhân viên
        </button>
      </div>
    </div>
    <div class="m-toolbar">
      <div class="m-toolbar-left m-col-10">
        <input
          type="text"
          class="m-icon-search m-input-search m-col-3"
          style="width: 250px"
          placeholder="Tìm kiếm theo Mã, Tên hoặc Số điện thoại"
        />

        <!-- <div id="cbxDepartment" class="mcombobox">
                    <input type="text" class="m-combobox">
                    <button class="m-combobox-button"> <i class="fa fa-chevron-down"></i></button>
                    <div class="m-combobox-data">


                    </div>
                </div> -->

        <div class="m-dropdown m-col-3">
          <div class="m-dropdown-text">Tất cả vị trí</div>
          <div class="m-dropdown-down">
            <i class="fas fa-chevron-down"></i>
          </div>
        </div>
      </div>
      <div class="m-toolbar-right">
        <button
          id="btnDeleteIcon"
          style="
            width: 50px;
            height: 40px;
            background-color: #f65454;
            display: none;
            border-radius: 4px;
            color: #ffffff;
            border: none;
          "
        >
          <i class="fa fa-trash" aria-hidden="true"></i>
        </button>
        <button
          onclick="LoadData()"
          class="m-second-button m-btn-refresh"
        ></button>
      </div>
    </div>
    <div class="m-content-main">
      <table id="tblEmployee" class="m-table" entityId="EmployeeId">
        <thead class="m-table m-text-left">
          <tr>
            <th fieldValue="EmployeeCode">Mã nhân viên</th>
            <th fieldValue="FullName">Họ và tên</th>
            <th fieldValue="GenderName">Giới tính</th>
            <th fieldValue="DateOfBirth" formatType="date">Ngày sinh</th>
            <th fieldValue="PhoneNumber">Điện thoại</th>
            <th fieldValue="Email">Email</th>
            <th fieldValue="Address">Địa chỉ</th>
            <th fieldValue="Salary" formatType="money">Mức lương cơ bản</th>
            <!-- <th fieldValue="DepartmentName">phòng ban</th> -->
            <!-- <th>Phòng ban</th> -->
            <!-- <th>Edit</th>
                        <th>Delete</th> -->
            <!-- <th>Tình trạng công việc</th> -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="customer in customers" :key="customer.customerId">
            <td>{{ customer.CustomerCode }}</td>
            <td>{{ customer.FullName }}</td>
            <td>{{ customer.Gender }}</td>
            <td>
              {{
                customer.DateOfBirth | formatDateOfBirth(customer.DateOfBirth)
              }}
            </td>
            <td>{{ customer.PhoneNumber }}</td>
            <td>{{ customer.Email }}</td>
            <td>{{ customer.Address }}</td>
            <td>
              {{ customer.DebitAmount | formatCurrency(customer.DebitAmount) }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="m-navigation">
      <div class="m-paging-left m-col-3">
        <div class="m-paging-text-left">Hiển thị 01-10/100 nhân viên</div>
      </div>
      <div class="m-paging-center m-col-6">
        <button class="m-btn-pagingFirst"></button>
        <button class="m-btn-pagingPrev"></button>
        <div class="m-paging-number">
          <div class="m-page">1</div>
          <div class="m-page">2</div>
          <div class="m-page">3</div>
          <div class="m-page">4</div>
          <div class="m-page">5</div>
          <div class="m-page">6</div>
        </div>
        <button class="m-btn-pagingNext"></button>
        <button class="m-btn-pagingLast"></button>
      </div>
      <div class="m-paging-right m-col-3">
        <div class="m-paging-text-right">10 nhân viên/ trang</div>
      </div>
    </div>
    <!-- modal  -->

    <div class="m-loadding">
      <div class="m-loadding-icon"></div>
    </div>
    <br />
    <CustomerDetail
      :isShow="isShowDialogDetail"
      @showDialog="showDialogParent"
      @loadData="loadData"
    />
    <!-- emit gọi đến @showdialog  -> gọi đến cha  -->
  </div>
</template>



<script>
import CustomerDetail from "./CustomerDetail.vue";
import axios from "axios";
export default {
  components: {
    CustomerDetail,
  },
  methods: {
    btnAddOnClick() {
      //document.getElementById('dlgPopup').style.display="block";
      this.showDialogParent(true);
    },
    showDialogParent(isShow) {
      this.isShowDialogDetail = isShow;
    },

    loadData() {
       axios
      .get(`http://cukcuk.manhnv.net/api/v1/Customerss`)
      .then((res) => {
        this.customers = res.data;
        console.log(res);
      })
      .catch((error) => console.log(error));
 
    },
  },

  data() {
    return {
      customers: [],
      isShowDialogDetail: false,
    };
  },
  filters: {
    formatDateOfBirth: function (data) {
      if (data) {
        const newDate = new Date(data);
        var day = newDate.getDate();
        day = day < 10 ? `0${day}` : day;
        var month = newDate.getMonth() + 1;
        month = month < 10 ? `0${month}` : month;
        var year = newDate.getFullYear();
        return `${day}/${month}/${year}`;
        // return year + "-" + month + "-" + day;
      }
    },
    formatCurrency(data) {
      if (data) {
        return Intl.NumberFormat("vi", {
          style: "currency",
          currency: "VND",
        }).format(data);
      }
    },
  },
  created() {
    axios
      .get(`http://cukcuk.manhnv.net/api/v1/Customerss`)
      .then((res) => {
        this.customers = res.data;
        console.log(res);
      })
      .catch((error) => console.log(error));
  },
};
</script>


<style scoped>
@import url("../../style/common/content.css");

@import url("../../style/common/toolbar.css");

@import url("../../style/common/grid.css");

@import url("../../style/common/table.css");

@import url("../../style/common/common.css");

@import url("../../style/common/navigation.css");

@import url("../../style/common/paging.css");

@import url("../../style/component/icon.css");

@import url("../../style/component/button.css");

@import url("../../style/component/dropdown.css");

@import url("../../style/component/input.css");

@import url("../../assets/font/fontawesome-5.15.4/css/all.min.css");
@import url("../../style/page/employee-info.css");
</style>
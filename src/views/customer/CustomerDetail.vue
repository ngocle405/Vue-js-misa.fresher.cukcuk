<template>
  <div class="">
    <div
      class="m-employee-form"
      id="dlgPopup"
      v-bind:class="{ 'm-dialog-show': isShow }"
    >
      <div class="m-employee-header">
        <div class="m-header-text">THÔNG TIN NHÂN VIÊN</div>
        <div class="m-btn-esc" id="btnCloseDialog" @click="btnCloseOnClick">
          <i class="fas fa-times"></i>
        </div>
      </div>
      <div class="m-employee-navbar">
        <div class="m-navbar-avatar">
          <div class="m-default-avatar"></div>
        </div>
        <div class="m-navbar-text">
          (Vui lòng chọn ảnh có định dạng .jpg. .jpeg. .png .gif.)
        </div>
      </div>
      <div class="m-employee-content">
        <div class="m-content-info">A. THÔNG TIN CHUNG:</div>
        <div class="m-underline-text"></div>
        <input
          class="m-datetime-text"
          id="txtEmployeeId"
          type="hidden"
          fieldName="EmployeeId"
        />
        <div class="m-content-row">
          <div class="m-employee-id">
            <div class="m-employee-text">Mã khách hàng (<span>*</span>)</div>
            <input
              type="text"
              id="txtEmployeeCode"
              class="m-input"
              placeholder="Nhập mã kh"
              v-model="customer.CustomerCode"
            />
          </div>
          <div class="m-employee-name">
            <div class="m-employee-text">Họ và tên (<span>*</span>)</div>
            <input
              type="text"
              id="txtEmployeeName"
              class="m-input"
              fieldName="FullName"
              placeholder="Nhập họ và tên khách hàng"
              v-model="customer.FullName"
              required
            />
          </div>
        </div>
        <div class="m-content-row">
          <div class="m-employee-birthday">
            <div class="m-employee-text">Ngày sinh</div>
            <div class="m-datetime-picker">
              <input
                class="m-datetime-text"
                id="dtDateOfBirth"
                fieldName="DateOfBirth"
                formatFormType="yyyymmdd"
                type="date"
                v-model="customer.DateOfBirth"
              />
            </div>
          </div>
          <div class="m-employee-gender">
            <div class="m-employee-text">Giới tính</div>
            <!-- <combobox id="cbxGender" fieldName="Gender" InputName="GenderName">
                            <item  value="1">nam</item>
                            <item  value="0">nữ</item>
                        </combobox> -->

            <!-- <div id="cbxGender" class="m-combobox" fieldName="Gender">
              <input type="text" class="m-combobox" fieldName="Gender" />
              <button class="m-combobox-button">
                <i class="fa fa-chevron-down"></i>
              </button>
              <div class="m-combobox-data">
                <div class="m-combobox-item" value="1">nam</div>
                <div class="m-combobox-item" value="0">nữ</div>
              </div>
           
            </div> -->
            <select name="" id="" class="m-combobox" v-model="customer.Gender">
              <option value="1">Nam</option>
              <option value="0">Nữ</option>
            </select>
          </div>
        </div>
        <div class="m-content-row">
          <div class="m-employee-citizenId">
            <div class="m-employee-text">Số tiền nợ (<span>*</span>)</div>
            <input
              type="text"
              class="m-input"
              placeholder="Nhập tiền nợ"
              v-model="customer.DebitAmount"
            />
          </div>
        </div>

        <div class="m-content-row">
          <div class="m-employee-email">
            <div class="m-employee-text">Email (<span>*</span>)</div>
            <input
              type="email"
              id="txtEmail"
              class="m-input"
              fieldName="Email"
              placeholder="Nhập Email"
              v-model="customer.Email"
            />
          </div>
          <div class="m-employee-phoneNumber">
            <div class="m-employee-text">Số điện thoại (<span>*</span>)</div>
            <input
              type="text"
              id="txtPhone"
              class="m-input"
              fieldName="PhoneNumber"
              placeholder="Nhập số điện thoại"
              v-model="customer.PhoneNumber"
              required
            />
          </div>
        </div>
        <div class="m-content-job">B. THÔNG TIN CÔNG VIỆC:</div>
        <div class="m-underline-text"></div>
        <div class="m-content-row">
          <div class="m-employee-position">
            <div class="m-employee-text">Ví trí</div>
            <!-- <combobox id="cbxPosition" api="http://cukcuk.manhnv.net/api/v1/Positions" InputName="PositionName" fieldName="PositionId" propertyDisplay="PositionName" propertyValue="PositionId">

                        </combobox> -->
          </div>
          <div class="m-document-dateRelease">
            <div class="m-lable">Phòng ban</div>
            <!-- <select name="" class="m-combobox" id="cbxDepartment" style="width: 190px;">
                            <option value="">Phòng hành chính</option>
                            <option value="">Phòng đào tạo</option>
                        </select> -->
            <!-- <combobox id="cbxDepartment" api="http://cukcuk.manhnv.net/api/v1/Departments" InputName="DepartmentName" fieldName="DepartmentId" propertyDisplay="DepartmentName" propertyValue="DepartmentId">

                        </combobox> -->

            <!-- <div id="cbxDepartment" scombobox  api="http://cukcuk.manhnv.net/api/v1/Departments" class="mcombobox"
                            fieldName="DepartmentId" propertyDisplay="DepartmentName" propertyValue="DepartmentId" fieldNameInput="DepartmentName">
                            <input type="text" class="m-combobox">
                            <button class="m-combobox-button"> <i class="fa fa-chevron-down"></i></button>
                            <div class="m-combobox-data">

                            </div>
                        </div> -->
          </div>
        </div>
      </div>
      <div class="m-employee-footer">
        <button id="btnCloseDialog" class="m-btn-cancel">Hủy</button>
        <button id="btn-save" class="m-btn-icon" @click="btnSaveOnClick()">
          <i class="far fa-save" style="padding-right: 8px"></i>Lưu lại
        </button>
       
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    //nhận cách thuộc tính từ lớp cha(customerlist)
    isShow: Boolean,
    CustomerId: String,
    customer: Object,
  },
  data() {
    return {
      // customer: {   },
      //  isShow:false
    };
  },
  methods: {
    /**
     * đóng form
     */
    btnCloseOnClick() {
      //emit gọi sự kiện showdialog
      this.$emit("showDialog", false);
    },
    /**
     * lưu dữ liệu
     */
    btnSaveOnClick() {
       this.$emit("save", this.customer);
      //
     
     
    },

    //
     btnUpdate(customer) {
       var me=this;
      axios
        .put(
          `http://cukcuk.manhnv.net/api/v1/Customerss/` + this.CustomerId,
          customer
        )
        .then(() => {
            alert("oke");
          //thêm thành công thì tự động đóng form
          me.$emit("showDialog", false);
          //sự kiện load dữ liệu
          me.$emit("loadData", false);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    //
     
  },

  //
  
};
</script>

<style>
.m-dialog-show {
  display: block !important;
}
@import url("../../style/page/employee-info.css");
@import url("../../style/component/combobox.css");
</style>
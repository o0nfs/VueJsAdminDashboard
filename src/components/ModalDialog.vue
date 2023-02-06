<template>
  <!-- FORM -->
  <el-form class="dialog__content overlay " v-show="show" ref="form" label-width="100px" size="small" :model="form">
    <el-form-item label="Edit">
    </el-form-item>
    <el-form-item label="Title" class="dialog__label" icon="el-icon-search">
      <el-input type="text" name="name-input" id="name-input"></el-input>
    </el-form-item>
    <!-- Type Input-->
    <i class="el-icon-message"></i>
    <el-form-item label="Type">
      <el-select v-model="value" multiple filterable remote reserve-keyword placeholder="Please enter a keyword" :remote-method="remoteMethod" :loading="loading">
        <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
        </el-option>
      </el-select>
    </el-form-item>
    <!-- Date input -->
    <el-form-item label="Date">
      <el-col :span="11">
        <el-date-picker type="date" placeholder="Pick a date" style="width: 100%;"></el-date-picker>
      </el-col>
    </el-form-item>
    <!-- Date input  /-->
    <!-- select publish or edit-->
    <el-form-item label="Status">
      <el-select v-model="formInline.region" placeholder="edit">
        <el-option label="edit" value="edit"></el-option>
        <el-option label="published" value="published"></el-option>
      </el-select>
    </el-form-item>
    <!-- select publish or edit  /-->
    <!-- Textarea Input -->
    <el-form-item label="Remark">
      <el-input type="textarea"></el-input>
    </el-form-item>
    <!-- Textarea Input  /-->
    <!-- cancel/confirm Buttons -->
    <el-form-item>
      <el-row>
        <el-button>Cancel</el-button>
        <el-button @click="confirm" class="dialog__confirm" type="primary">Confirm</el-button>
      </el-row>
    </el-form-item>
    <!-- cancel/confirm Buttons /-->
  </el-form>
</template>


<script>
  export default {
    data() {
      return {
        //Textarea Input
        textarea: '',
        //select publish or edit
        formInline: {
          region: ''
        },
        //Date input
        pickerOptions: {
          disabledDate(time) {
            return time.getTime() > Date.now();
          },
          shortcuts: [{
            text: 'Today',
            onClick(picker) {
              picker.$emit('pick', new Date());
            }
          }, {
            text: 'Yesterday',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit('pick', date);
            }
          }, {
            text: 'A week ago',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', date);
            }
          }]
        },
        value1: '',
        value2: '',
        //Type input  
        options: [{
          value: 'Option1',
          label: 'Option1'
        }, {
          value: 'Option2',
          label: 'Option2'
        }, {
          value: 'Option3',
          label: 'Option3'
        }, {
          value: 'Option4',
          label: 'Option4'
        }, {
          value: 'Option5',
          label: 'Option5'
        }],
        value: ''
      }
    },
    options: [],
    value: [],
    list: [],
    loading: false,
    states: ["Alabama", "Alaska", "Arizona",
      "Arkansas", "California", "Colorado",
      "Connecticut", "Delaware", "Florida",
      "Georgia", "Hawaii", "Idaho", "Illinois",
      "Indiana", "Iowa", "Kansas", "Kentucky",
      "Louisiana", "Maine", "Maryland",
      "Massachusetts", "Michigan", "Minnesota",
      "Mississippi", "Missouri", "Montana",
      "Nebraska", "Nevada", "New Hampshire",
      "New Jersey", "New Mexico", "New York",
      "North Carolina", "North Dakota", "Ohio",
      "Oklahoma", "Oregon", "Pennsylvania",
      "Rhode Island", "South Carolina",
      "South Dakota", "Tennessee", "Texas",
      "Utah", "Vermont", "Virginia",
      "Washington", "West Virginia", "Wisconsin",
      "Wyoming"
    ],
    props: ['show', 'title', 'description', 'cancel', 'confirm', 'name', 'label', 'typeZone'],
    mounted() {
      this.list = this.states.map(item => {
        return {
          value: `value:${item}`,
          label: `label:${item}`
        };
      });
    },
    methods: {
      remoteMethod(query) {
        if (query !== '') {
          this.loading = true;
          setTimeout(() => {
            this.loading = false;
            this.options = this.list.filter(item => {
              return item.label.toLowerCase()
                .indexOf(query.toLowerCase()) > -1;
            });
          }, 200);
        } else {
          this.options = [];
        }
      }
    }
  }
</script>

<style>
  .dialog__content {
    background: #FFFFFF;
    box-shadow: 0px 1px 15px 0.01px;
    border-radius: 15px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: left;
    position: relative;
    top: -100px;
    z-index: 1;
    width: 700px;
    padding: 40px;
    margin: 0 auto;
  }
</style>
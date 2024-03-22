<template>
  <VueDatePicker
      ref="datepicker"
      month-name-format="long"
      @date-update="selectDate"
      v-model="date"
      :model-value="date"
      @update:model-value="selectDates"
      :format="format"
      placeholder="mm/dd/yyyy"
      :min-date="minDate ? minDate : ''"
      :max-date="maxDate ? maxDate : ''"
  >
    <template #action-preview="{ value }">
      <div class="action-preview">
        {{ getValue(value) }}
      </div>
    </template>
  </VueDatePicker>
</template>
<script>
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

export default {
  name: 'TestTaskDatePicker',
  components: {VueDatePicker},
  methods: {
    selectDate(date) {
      this.$refs.datepicker.updateInternalModelValue(date)
      this.$refs.datepicker.selectDate()
      this.date = this.getInputValue(this.date)
    },
    getValue(val) {
      return val ? val.getDate() + ' ' + this.months[val.getMonth()] + ', ' + val.getFullYear() : ''
    },
    getInputValue(val) {
      return val ? val.split(',')[0] : ''
    },
    selectDates(modelData) {
      this.$emit('getDate', modelData, this.dateType)
    },
    format(date) {
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();
      return `${month}/${day}/${year}`;
    }
  },
  data() {
    return {
      date: null,
      months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    }
  },
  props: {
    dateType: {
      required: true,
      type: String
    },
    minDate: {
      required: false,
      type: String || null
    },
    maxDate: {
      required: false,
      type: String || null
    }
  }
}
</script>
<style>
.dp__month_year_select:hover {
  background: none;
  pointer-events: none;
  cursor: default;
}
.dp__month_year_wrap:hover {
  cursor: default;
}

.dp--tp-wrap {
  display: none;
}

.dp__today {
  border: unset;
  border-radius: 50%;
  background: #e6e6e6;
}

.dp__active_date {
  background: #222222;
  color: white;
  border-radius: 50%;
}

.dp__month_year_select {
  width: unset;
}

.dp__month_year_wrap {
  justify-content: center;
}

.dp__outer_menu_wrap {
  border-radius: 10px;
}

.dp__menu {
  border-radius: 10px;
  -moz-box-shadow: 0 0 30px #ccc;
  -webkit-box-shadow: 0 0 30px #ccc;
  box-shadow: 0 0 30px #ccc;
}

.dp__menu_inner {
  width: 330px;
}

.dp__inner_nav {
  color: grey;
}

.dp--year-select, .dp__month_year_select {
  cursor: default;
}

.dp__calendar_header_item {
  font-weight: 500;
}

.dp__calendar_header_separator {
  display: none;
}

.dp__action_row {
}

.dp__action_buttons {
  display: none;
}

.action-preview {
  width: 300px;
  height: 30px;
  color: black;
  position: absolute;
  top: 50px;
  left: 15px;
  border-radius: 5px;
  border: 1px solid #e6e6e6;
  padding-left: 10px;
  font-size: 15px;
}

.dp__month_year_row {
  margin-bottom: 50px;
}
</style>
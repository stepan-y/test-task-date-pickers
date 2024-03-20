<template>
  <div class="main__wrapper">
    <div class="main">
      <div class="main__title">
        Settings
      </div>
      <div class="main__input-field">
        <div class="input-name">
          Start date
        </div>
        <div class="input">
          <TestTaskDatePicker :date-type="'startDate'" @getDate="getDate" :max-date="cutOffDate">
          </TestTaskDatePicker>
        </div>
      </div>
      <div class="main__input-field">
        <div class="input-name">
          Cut off Date & Time
        </div>
        <div class="input">
          <TestTaskDatePicker :date-type="'finishDate'" @getDate="getDate" :min-date="startDate">
          </TestTaskDatePicker>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import TestTaskDatePicker from "@/components/TestTaskDatePicker.vue";

export default {
  name: 'TestTaskComponent',
  components: {
    TestTaskDatePicker,
  },
  data () {
    return {
      startDate: null,
      cutOffDate: null
    }
  },
  methods: {
    getDate(value, type) {
      if (type === 'startDate') {
        this.startDate = value
      } else {
        this.cutOffDate = value
      }
    }
  }
}
</script>
<style>
.main__wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.main {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.main__title {
  font-weight: 600;
  font-size: 20px;
}

.main__input-field {
  display: flex;
  flex-direction: row;
  gap: 20px;
  align-items: center;
}

.input-name {
  font-size: 16px;
}

</style>
<template>
  <div class="booking-seats-page">
    <div class="block has-foot">
      <div class="row border-b-1px">
        <span class="key">姓名</span>
        <span class="value">{{userInfo.username}}</span>
      </div>
      <div class="row border-b-1px">
        <span class="key">工号</span>
        <span class="value">{{userInfo.jobnumber}}</span>
      </div>
      <div class="row border-b-1px">
        <span class="key">部门</span>
        <span class="value">{{userInfo.departmentname}}</span>
      </div>
      <div class="row border-b-1px">
        <span class="key">岗位</span>
        <span class="value">{{userInfo.position}}</span>
      </div>
      <div class="row border-b-1px">
        <span class="key">预约座位</span>
        <span class="right" @click="bookingSeats">
          <span v-if="seatsNum" class="value">{{seatsNum}}</span>
          <span v-else class="please">请选择</span>
          <span class="icon icon-forward"></span>
        </span>
      </div>
      <div class="row border-b-1px">
        <span class="key">预约时段</span>
        <span class="right">
          <el-date-picker
                  class="value"
                  type="dates"
                  v-model="date"
                  placeholder="可多选"
                  :aaa="aaa"
                  :disabled-dates="disabledDates"
                  :picker-options="pickerOptions">
          </el-date-picker>
          <span class="icon icon-forward"></span>
        </span>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    data () {
      return {
        userInfo: {},
        seatsNum: '',
        date: '',
        aaa: '1234567',
        pickerOptions: this.setPickerOptionsr(),
        duration: '自动计算'
      }
    },
    methods: {
      bookingSeats () {
        this.$router.push('/map-seats')
      },
      setPickerOptionsr () {
        return {
          // 今天以前的日期不能选
          disabledDate (time) {
            // let now = Date.now()
            // return time.toLocaleDateString() === '2019/6/20'
            let t = new Date('2019/06/22')
            // console.log(time.toLocaleString())
            return time.getTime() === t.getTime()
          },
          disabledDates: [
            {
              date: '2019/06/21',
              used: [1, 0]
            },
            {
              date: '2019/06/22',
              used: [0, 1]
            },
            {
              date: '2019/06/23',
              used: [1, 1]
            }
          ]
        }
      }
    }
  }
</script>

<style lang="scss">
  .booking-seats-page {
    background-color: #f8f8f8;
  }
</style>

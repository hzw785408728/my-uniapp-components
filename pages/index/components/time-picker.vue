<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<template>
  <view>
      <view class="uni-padding-wrap">
          <!-- 通过 state 访问属性 -->
          <view class="uni-title">日期：{{state.year}}年{{state.month}}月{{state.day}}日</view>
          <text @tap="handlePopup">选择日期</text>
          <view class="uni-list-cell-db">
					<!-- <picker mode="time" :value="time" start="09:01" end="21:01" @change="bindTimeChange">
						<view class="uni-input">{{time}}</view>
					</picker> -->
					<view class="uni-input" @tap="handlePopup">{{time}}</view>
				</view>
      </view>
        <!-- 通过 state 访问属性 -->

      <uni-popup
        ref="popupRef"
        :title="state.title"
        type="bottom"
      >
      <view>123</view>
      <picker-view indicator-class="indicator" :value="state.value" @change="bindChange" class="picker-view">
          <picker-view-column>
              <view class="item" v-for="(item,index) in state.years" :key="index">{{item}}年</view>
          </picker-view-column>
          <picker-view-column>
              <view class="item" v-for="(item,index) in state.months" :key="index">{{item}}月</view>
          </picker-view-column>
          <picker-view-column>
              <view class="item" v-for="(item,index) in state.days" :key="index">{{item}}日</view>
          </picker-view-column>
      </picker-view>
      </uni-popup>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

const popupRef = ref(null);
const state = reactive({
    title: 'picker-view',
    years: [],
    year: 0,
    months: [],
    month: 0,
    days: [],
    day: 0,
    value: [9999, 0, 0],
    visible: false,
});
const time = ref('09:01');
const indicatorStyle = {
  height: '50px',
  fontWeight:'blod',
  fontSize:'100rpx',
  color:'red'
};

const date = new Date();
state.year = date.getFullYear();
state.month = date.getMonth() + 1;
state.day = date.getDate();

for (let i = 1990; i <= state.year; i++) {
    state.years.push(i);
}
for (let i = 1; i <= 12; i++) {
    state.months.push(i);
}
for (let i = 1; i <= 31; i++) {
    state.days.push(i);
}

state.value = [state.years.indexOf(state.year), state.month - 1, state.day - 1];

const bindChange = (e: any) => {
    const val = e.detail.value;
    state.year = state.years[val[0]];
    state.month = state.months[val[1]];
    state.day = state.days[val[2]];
};

const handlePopup = () => {
  console.log('====================================');
  console.log(popupRef.value);
  console.log('====================================');
  // 弹出选择器
  popupRef.value&&popupRef.value.open();
};
</script>

<style lang="scss">
	.picker-view {
		width: 750rpx;
		height: 600rpx;
		margin-top: 20rpx;
	}
	.item {
		line-height: 100rpx;
		text-align: center;
}
.indicator {
  height: 50px;
  font-weight: bold;
  font-size: 100rpx;
  color: red;
}
</style>

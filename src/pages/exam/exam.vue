<script lang="ts" setup>
import { reactive, computed, ref } from 'vue';

// 题库数据
const questionBank = reactive([
  {
    question: "在 IPv4地址段 10.20.30.0/24中，划分至少3个子网，其主机位数最长是(1)位，其子网掩码是(2)。",
    options: ["7", "8", "5", "6"],
    correctIndex: 0,
  },
  {
    question: "在 IPv4地址段 10.20.30.0/24中，划分至少3个子网，其主机位数最长是(1)位，其子网掩码是(2)。",
    options: ["255.255.255.224", "255.255.255.128", "255.255.255.192", "255.255.255.0"],
    correctIndex: 1,
  },
]);

// 当前题目索引
const currentIndex = ref(0);

// 当前题目
const currentQuestion = computed(() => questionBank[currentIndex.value]);

// 是否是第一题或最后一题
const isFirstQuestion = computed(() => currentIndex.value === 0);
const isLastQuestion = computed(() => currentIndex.value === questionBank.length - 1);

// 方法：选择答案
const selectOption = (index: number) => {
  if (index === currentQuestion.value.correctIndex) {
    uni.showToast({
      title: "回答正确！",
      icon: "success",
    });
  } else {
    uni.showToast({
      title: "回答错误！",
      icon: "error",
    });
  }
};

// 方法：跳到下一题
const nextQuestion = () => {
  if (!isLastQuestion.value) {
    currentIndex.value++;
  }
};

// 方法：跳到上一题
const prevQuestion = () => {
  if (!isFirstQuestion.value) {
    currentIndex.value--;
  }
};
</script>

<template>
  <view class="container">
    <view class="question">
      {{ currentIndex + 1 }}: 单选题
    </view>
    <view class="question">
      {{ currentQuestion.question }}
    </view>
    <view class="options">
      <button
        v-for="(option, index) in currentQuestion.options"
        :key="index"
        class="option"
        @click="selectOption(index)"
      >
        {{ String.fromCharCode('A'.charCodeAt(0) + index) }}: {{ option }}
      </button>
    </view>
    <view class="navigation">
      <button class="prev-button" @click="prevQuestion" :disabled="isFirstQuestion">
        上一题
      </button>
      <button class="next-button" @click="nextQuestion" :disabled="isLastQuestion">
        下一题
      </button>
    </view>
  </view>
</template>

<style scoped>
.container {
  padding: 20rpx;
  display: flex;
  flex-direction: column;
  height: calc(100vh - 88rpx - 40rpx);
}

.question {
  font-size: 32rpx;
  font-weight: bold;
  margin-bottom: 20rpx;
  color: #666;
}

.options {
  display: flex;
  flex-direction: column;
  gap: 10rpx;
}

.option {
  padding: 20rpx;
  font-size: 28rpx;
  text-align: center;
  border-radius: 10rpx;
  background-color: #f0f0f0;
  display: block;
  width: 100%;
  height: 100rpx;
  margin-top: 10px;
}
.option:active {
  background-color: #dcdcdc;
}

.navigation {
  display: flex;
  justify-content: space-between;
  margin-top: auto;
}

.prev-button,
.next-button {
  padding: 20rpx;
  font-size: 28rpx;
  text-align: center;
  border-radius: 10rpx;
  background-color: #4caf50;
  color: white;
  flex: 1;
  margin: 0 10rpx;
}
.prev-button:disabled,
.next-button:disabled {
  background-color: #dcdcdc;
  color: #888888;
}
</style>

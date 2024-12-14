<template>
  <view class="container">
    <view class="card-list">
      <!-- 试卷卡片 -->
      <view
        v-for="(paper, index) in papers"
        :key="index"
        class="card"
        @click="navigateToQuestion(index)"
      >
        <text class="card-desc">{{ paper.description }}</text>
      </view>

      <!-- 加号卡片 -->
      <view class="card add-card" @click="addNewPaper">
        <text class="add-icon">+</text>
      </view>
    </view>
  </view>
</template>

<script lang="ts" setup>
// 试卷数据
const papers = [
  { id: "试卷 1", description: "2024年11月网络工程师考试试题上午题" },
  { id: "试卷 2", description: "2024年5月网络工程师考试试题上午题" },
];

// 跳转到答题页面
const navigateToQuestion = () => {
  uni.navigateTo({
    url: `/pages/exam/exam`,
  });
};

// 占位方法：点击加号卡片
const addNewPaper = () => {
  uni.showToast({
    title: "功能尚未实现",
    icon: "none",
  });
};
</script>

<style scoped>
.container {
  padding: 20rpx;
}

.card-list {
  display: flex;
  flex-direction: column;
  gap: 20rpx;
}

/* 普通卡片样式 */
.card {
  height: 120rpx;
  padding: 20rpx;
  background-color: #f7f7f7;
  border-radius: 10rpx;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-desc {
  font-size: 32rpx;
  font-weight: bold;
  color: #666;
  margin-top: 10rpx;
}

.card:active {
  background-color: #eaeaea;
}

/* 加号卡片样式 */
.add-card {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10rpx;
  border: 2rpx dashed #bbbbbb;
  height: 120rpx;
}

.add-icon {
  font-size: 48rpx;
  color: #bbbbbb;
  font-weight: bold;
}
</style>

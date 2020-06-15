<template>
  <div class="home">
    <div class="left section">
      <div class="search">
        <el-input type="primary" size="mini" placeholder="搜索">
          <i slot="prefix" class="el-input__icon el-icon-search"></i>
        </el-input>
      </div>
      <ul class="menu-list">
        <li
          class="menu-item"
          :class="{ active: item.value === currentValue }"
          v-for="item in menu"
          :key="item.value"
          @click="currentValue = item.value"
        >
          <i class="menu-icon" :class="[item.icon]"></i>
          <span>{{ item.label }}</span>
        </li>
      </ul>
    </div>
    <div class="right section task-detail">
      <div class="task">
        <div class="task-title">
          <h1>{{ currentLabel }}</h1>
          <p>{{ $moment().format("M月DD日 dddd") }}</p>
        </div>
      </div>
      <div class="add-task">
        <el-input placeholder="添加任务" v-model="task">
          <i slot="prefix" class="el-input__icon el-icon-plus"></i>
        </el-input>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      currentValue: 1,
      task: "",
      menu: [
        {
          label: "我的一天",
          icon: "el-icon-sunny",
          value: 1,
        },
        // {
        //   label: '重要',
        //   icon: 'el-icon-star-off',
        //   value: 2
        // },
        // {
        //   label: '已计划日程',
        //   icon: 'el-icon-date',
        //   value: 3
        // }
      ],
    };
  },
  computed: {
    currentLabel() {
      return this.menu.find((i) => i.value === this.currentValue).label;
    },
  },
};
</script>
<style lang="less">
@menuListWidth: 260px;
@bgGray-6: #666;
@bgGray-e: #eee;
@bgGray-d: #ddd;
@black: #000;
@white: #fff;
@taskTitle: #d8a;
.home {
  font-family: monospace;
  font-size: 14px;
  overflow-x: hidden;

  .section {
    box-sizing: border-box;
    position: absolute;
    top: 0;
    bottom: 0;
  }
  .left {
    margin-top: 30px;
    width: @menuListWidth;
    float: left;
    .el-input {
      .el-input__inner {
        background: @bgGray-e;
        &::-webkit-input-placeholder {
          color: @black;
        }
      }
      .el-input__prefix .el-input__icon {
        color: @black;
      }
    }
  }
  .right {
    padding: 24px 14px;
    width: calc(100% - @menuListWidth);
    margin-left: @menuListWidth;
    background: url("../../assets/images/background.jpg") no-repeat;
    background-size: 100% 100%;
    .task-title {
      color: @taskTitle;
    }
    .add-task {
      position: absolute;
      bottom: 16px;
      left: 20px;
      right: 20px;
      .el-input {
        .el-input__inner {
          background: @bgGray-6;
          border-color: @bgGray-6;
          padding-left: 50px;
          caret-color: @black;
          color: @white;
          &::-webkit-input-placeholder {
            color: @white;
          }
        }
        .el-input__prefix .el-input__icon {
          color: @white;
        }
      }
    }
  }
  .search {
    padding: 0 15px;
  }

  .menu-list {
    margin-top: 8px;
  }
  .menu-item {
    display: flex;
    align-items: center;
    padding: 4px 20px;
    cursor: pointer;
    &.active {
      background: @bgGray-d;
    }
  }
  .menu-icon {
    margin-right: 8px;
    font-size: 18px;
  }
}
</style>

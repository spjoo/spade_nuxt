<template>
  <div class="tab_wrap" ref="tab_wrap">
    <div
      class="tab_menu"
      ref="tab_menu"
    >
      <ul
        ref="tab_menu_list"
        class="tab_menu_list"
      >
        <li
          v-for="(item, index) in tabData"
          ref="tab_menu_item"
          class="tab_menu_item"
          :class="item.name === activeTab ? 'is_active' : ''"
          :key="item.name + item.id"
        >
          <button class="tab_menu_btn" @click="onClickTab(item.name, index)">
            {{ item.name }}
          </button>
        </li>
      </ul>
    </div>
    <div class="tab_content_wrap">
      <div v-show="activeTabContent === 0" class="tab_content tab_content_01">
        Tab 01
      </div>
      <div v-show="activeTabContent === 1" class="tab_content tab_content_02">
        Tab 02
      </div>
      <div v-show="activeTabContent === 2" class="tab_content tab_content_03">
        Tab 03
      </div>
      <div v-show="activeTabContent === 3" class="tab_content tab_content_04">
        Tab 04
      </div>
      <div v-show="activeTabContent === 4" class="tab_content tab_content_05">
        Tab 05
      </div>
      <div v-show="activeTabContent === 5" class="tab_content tab_content_06">
        Tab 06
      </div>
      <div v-show="activeTabContent === 6" class="tab_content tab_content_07">
        Tab 07
      </div>
      <div v-show="activeTabContent === 7" class="tab_content tab_content_08">
        Tab 08
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabList",
  data() {
    return {
      tabPosition: {
        moveX: 0,
        moveY: 0
      },
      tabWidth: 0,
      tabListWidth: 0,
      activeTab: "",
      activeTabContent: 0,
      tabData: [
        {
          id: 0,
          name: "1:1 문의 내역"
        },
        {
          id: 1,
          name: "상품 Q&A 내역"
        },
        {
          id: 2,
          name: "지인톡 상담 내역"
        },
        {
          id: 3,
          name: "인테리어 상담"
        },
        {
          id: 4,
          name: "1:1 문의 내역2"
        },
        {
          id: 5,
          name: "상품 Q&A 내역2"
        },
        {
          id: 6,
          name: "지인톡 상담 내역2"
        },
        {
          id: 7,
          name: "인테리어 상담2"
        }
      ]
    };
  },
  methods: {
    onClickTab(item, index) {
      if (this.activeTab === item) return;
      this.activeTab = item;
      this.activeTabContent = index;
      if (this.tabListWidth > this.tabWidth && index > 0) {
        let moveX = 0;
        for (let i = 0; i < this.tabData.length; i++) {
          if (i === index - 1) break;
          moveX += this.$refs.tab_menu_item[i].clientWidth;
        }
        if (moveX > this.tabListWidth - this.tabWidth)
          moveX = this.tabListWidth - this.tabWidth;
        this.$refs.tab_menu_list.scrollLeft = moveX;
      }
    },
  },
  created() {
    this.activeTab = this.tabData[0].name;
    this.activeTabContent = 0;
  },
  mounted() {
    if (
      this.$refs.tab_menu_list.scrollWidth > this.$refs.tab_menu.clientWidth
    ) {
      this.$refs.tab_wrap.classList.add("is_scroll")
    }
    this.tabWidth = this.$refs.tab_menu.clientWidth;
    this.tabListWidth = this.$refs.tab_menu_list.scrollWidth;
    console.log(this.tabWidth, this.tabListWidth, this.$device);
  },
};
</script>

<style scoped>
.tab_wrap {
  padding: 0 10px;
  width: 100%;
  overflow: hidden;
}
.tab_menu {
  border-top: 1px solid #e2e2e2;
  border-bottom: 1px solid #e2e2e2;
  touch-action: none;
}
.tab_menu_list {
  white-space: nowrap;
  padding: 0;
  scroll-behavior: smooth;
  text-align: left;
}
.tab_menu_item {
  display: inline-block;
  vertical-align: top;
  list-style: none;
}
.tab_content {
  padding-top: 25px;
}
.tab_menu_btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 40px;
  padding: 0 17px;
  font-size: 14px;
  font-weight: 400;
  background: none;
  border: 0;
  margin: -1px 0;
  cursor: pointer;
  white-space: nowrap;
}
.tab_wrap.is_scroll {
  padding: 0;
}
.is_scroll .tab_menu {
  border-top: 0;
  border-bottom: 0;
}
.is_scroll .tab_menu_list {
  padding: 0 10px;
  overflow-y: hidden;
  overflow-x: scroll;
}
.is_scroll .tab_menu_btn {
  margin: 0;
  border-top: 1px solid #e2e2e2;
  border-bottom: 1px solid #e2e2e2;
}
.is_active .tab_menu_btn {
  background: #b49277;
  border-color: #b49277;
  color: #fff;
}
</style>

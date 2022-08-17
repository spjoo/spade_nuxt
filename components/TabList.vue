<template>
  <div ref="tab_wrap" class="tab_wrap">
    <div
      class="tab_menu"
      @mousemove="onMoveTab"
      @mousedown.prevent="onMoveStartTab"
      @mouseup.prevent="onMoveEndTab"
      @touchmove="onMoveTab"
      @touchstart="onMoveStartTab"
      @touchend="onMoveEndTab"
    >
      <ul
        ref="tab_menu_list"
        class="tab_menu_list"
        :class="[
          tabMoveStart ? 'is_move_start' : '',
          tabMoved ? 'is_moved' : ''
        ]"
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
        pointX: 0,
        pointY: 0,
        moveX: 0,
        moveY: 0
      },
      tabMoveStart: false,
      tabMoved: false,
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
      if (this.tabMoved || this.activeTab === item) return;
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
        this.$refs.tab_menu_list.style.transform = `translateX(-${moveX}px)`;
        this.tabPosition.moveX = moveX;
      }
    },
    onMoveTab(e) {
      if (this.tabMoveStart && this.tabListWidth > this.tabWidth) {
        let moveX;
        if (this.$device.isDesktop) {
          moveX =
            this.tabPosition.moveX - (this.tabPosition.pointX - e.clientX);
        } else if (this.$device.isMobile) {
          moveX =
            this.tabPosition.moveX -
            (this.tabPosition.pointX - e.changedTouches[0].pageX);
        }
        if (moveX > 0) moveX = 0;
        else if (Math.abs(moveX) > this.tabListWidth - this.tabWidth)
          moveX = (this.tabListWidth - this.tabWidth) * -1;
        const translateX = `translateX(${moveX}px)`;
        this.$refs.tab_menu_list.style.transform = translateX;
        if (!this.tabMoved) this.tabMoved = true;
      }
    },
    onMoveStartTab(e) {
      if (!this.tabListWidth > this.tabWidth) return;
      if (this.$device.isDesktop) {
        this.tabPosition.pointX = e.clientX;
      } else if (this.$device.isMobile) {
        // 모바일에서 click 된 경우 touchstart 이벤트도 같이 실행되면서 오류 발생 - optional chaining 처리
        this.tabPosition.pointX = e.changedTouches?.[0].pageX;
      }
      if (this.tabPosition.moveX !== 0) {
        const style = getComputedStyle(this.$refs.tab_menu_list);
        const matrix = new WebKitCSSMatrix(style.transform);
        this.tabPosition.moveX = matrix.m41;
      }
      this.tabMoveStart = true;
    },
    onMoveEndTab() {
      const style = getComputedStyle(this.$refs.tab_menu_list);
      const matrix = new WebKitCSSMatrix(style.transform);
      this.tabPosition.moveX = matrix.m41;
      this.tabMoveStart = false;
      setTimeout(() => {
        // 탭 무브가 끝난 후 버튼 클릭되는 현상 때문에 tabMoved = false 값은 비동기로 처리
        this.tabMoved = false;
      }, 0);
    }
  },
  created() {
    this.activeTab = this.tabData[0].name;
    this.activeTabContent = 0;
  },
  mounted() {
    if (this.$device.isDesktop)
      window.addEventListener("mouseup", this.onMoveEndTab);
    if (
      this.$refs.tab_menu_list.scrollWidth > this.$refs.tab_wrap.clientWidth
    ) {
      this.$refs.tab_wrap.classList.add("is_scroll")
      this.$refs.tab_menu_item.forEach(v => {
        v.style.flexBasis = "33.333%";
        v.style.flexGrow = "0";
        v.style.flexShrink = "0";
      });
    }
    this.tabWidth = this.$refs.tab_wrap.clientWidth;
    this.tabListWidth = this.$refs.tab_menu_list.scrollWidth;
    console.log(this.tabWidth, this.tabListWidth, this.$device);
  },
  beforeDestroy() {
    if (this.$device.isDesktop)
      window.removeEventListener("mouseup", this.onMoveEndTab);
  },
};
</script>

<style scoped>
.tab_wrap {
  margin: 0 10px;
  overflow: hidden;
}
.tab_menu {
  border-top: 1px solid #e2e2e2;
  border-bottom: 1px solid #e2e2e2;
  touch-action: none;
  overflow: hidden;
}
.tab_menu_list {
  padding: 0;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  transition: 0.5s ease transform;
}
.tab_menu_list.is_move_start {
  transition: none;
}
.tab_menu_item {
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
  margin: -1px 0;
  height: 40px;
  padding: 0 17px;
  font-size: 14px;
  font-weight: 400;
  background: none;
  border: 0;
  cursor: pointer;
  white-space: nowrap;
}
.is_scroll .tab_menu_btn {
  padding: 0 5px;
}
.is_active .tab_menu_btn {
  background: #b49277;
  color: #fff;
}
</style>

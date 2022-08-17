<template>
  <nav id="gnb">
    <ul class="gnb_list">
      <li v-for="item in menuData" class="gnb_item" :class="activeMenu === item.name ? 'is_active': ''" :key="item.name + item.id">
        <a href="#" class="gnb_link" @click="onClickMenu(item.name)">{{ item.name }}</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "Gnb",
  data() {
    return {
      activeMenu: "",
      menuData: [
        {
          id: 0,
          name:"정보보안 설비",
        },
        {
          id: 1,
          name:"개인정보제공",
        },
        {
          id: 2,
          name:"비식별조치검증",
        },
      ]
    }
  },
  created() {
    this.activeMenu = this.menuData[0].name;
  },
  methods: {
    onClickMenu(item) {
      this.activeMenu = item;
    }
  }
}
</script>

<style scoped>
.gnb_list {
  padding-left: 11px;
}
.gnb_item {
  position: relative;
  list-style: none;
}
.gnb_link {
  position: relative;
  display: flex;
  align-items: center;
  padding-left: 20px;
  height: 53px;
  font-size: 16px;
  font-weight: 400;
  color: #D0DDF2;
  border-radius: 10px 0 0 10px;
}
/* box-shadow 속성은 자기 자신한테는 영향을 끼치지 않는다 안쪽에 적용하지 않은 경우 */
.is_active .gnb_link:before,
.is_active .gnb_link:after {
  display: block;
  content: '';
  position: absolute;
  right: 0;
  width: 50px;
  height: 50px;
  background: transparent;
  border-radius: 50%;
}
.is_active .gnb_link:before {
  bottom: 100%;
  box-shadow: 25px 25px 0 #fff;
}
.is_active .gnb_link:after {
  top: 100%;
  box-shadow: 25px -25px 0 #fff;
}
.is_active .gnb_link {
  background-color: #fff;
  font-weight: bold;
  color: #2B2B2B;
}

/*.is_active .box_after,*/
/*.is_active .box_before {*/
/*  position: absolute;*/
/*  right: 0;*/
/*  width: 25px;*/
/*  height: 25px;*/
/*  background-color: #fff;*/
/*}*/
/*.is_active .box_before {*/
/*  top: -25px;*/
/*}*/
/*.is_active .box_after {*/
/*  bottom: -25px;*/
/*}*/
/*.is_active .box_before:before,*/
/*.is_active .box_after:before {*/
/*  content: '';*/
/*  position: absolute;*/
/*  left: 0;*/
/*  top: 0;*/
/*  right: 0;*/
/*  bottom: 0;*/
/*  background-color: #33476D;*/
/*}*/
/*.is_active .box_before:before {*/
/*  border-radius: 0 0 25px 0;*/
/*}*/
/*.is_active .box_after:before {*/
/*  border-radius: 0 25px 0 0;*/
/*}*/
</style>

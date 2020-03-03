<template>
  <div class="q-pa-md">
    <q-field
      ref="city"
      filled
      v-model="city"
      label="地区"
      stack-label
      :rules="[val => !!'请选择' || 'Field is required']"
    >
      <template v-slot:prepend>
        <q-icon name="place" />
      </template>
      <template v-slot:control>
        <div class="full-width no-outline">
          <span @click="toAddress">{{ city }}</span>
          <!-- 三级联动插件-->
          <v-distpicker type="mobile" @selected="selected" v-show="addInp">
          </v-distpicker>
        </div>
      </template>
      <template v-slot:append>
        <q-icon name="close" class="cursor-pointer" @click="toReset" />
      </template>
    </q-field>
  </div>
</template>

<script>
import VDistpicker from "v-distpicker";
export default {
  name: "HomeHeader",
  data() {
    return {
      //定义data数据
      city: "请选择",
      addInp: false
    };
  },
  components: {
    VDistpicker
  },
  methods: {
    toReset() {
      this.city = "请选择";
      this.addInp = false;
    },
    reset() {
      this.$refs.city.resetValidation();
    },
    // 点击弹出三级联动
    toAddress() {
      this.addInp = true;
    },
    // 省市区三级联动
    selected(data) {
      this.addInp = false;
      this.city =
        data.province.value + " " + data.city.value + " " + data.area.value;
    }
  }
};
</script>
<style scoped></style>

<template>
  <div class="home">
    <van-search v-model="serchData" placeholder="商品搜索共239款" input-align="center" />

    <van-swipe :autoplay="3000" :height="200" :width="375">
      <van-swipe-item v-for="(images, index) in images" :key="index">
        <img class="swiperimg" contain v-lazy="images.image_url" />
      </van-swipe-item>
    </van-swipe>

    <van-grid :column-num="5">
      <van-grid-item
        v-for="(item,index) in channel"
        :key="index"
        :icon="item.icon_url"
        :text="item.name"
      />
    </van-grid>

    <div class="brandList">
      <van-panel title="品牌制造直供商">
        <van-grid :column-num="2">
          <van-grid-item v-for="(item1,index1) in brandList" :key="index1">
            <van-image fit="cover" laxy lode :src="item1.new_pic_url" />
            <h4 class="title">{{item1.name}}</h4>
            <p class="price">{{item1.floor_price}}元起</p>
          </van-grid-item>
        </van-grid>
      </van-panel>
    </div>

    <div class="newGoodsList">
      <van-panel title="品牌制造直供商">
        <van-grid :column-num="2">
          <van-grid-item v-for="(item2,index2) in newGoodsList" :key="index2">
            <van-image fit="cover" laxy lode :src="item2.list_pic_url" />
            <h4 class="title van-ellipsis">{{item2.name}}</h4>
            <p class="price van-ellipsis">{{item2.retail_price}}元起</p>
          </van-grid-item>
        </van-grid>
      </van-panel>
    </div>

    <div class="hotGoodsList">
      <van-panel title="人气推荐">
        <van-card
          v-for="(item3,index3) in hotGoodsList"
          :key="index3"
          :price="item3.retail_price"
          :desc="item3.goods_brief"
          :title="item3.name"
          :thumb="item3.list_pic_url"
        />
      </van-panel>
    </div>

    <div style="height:50px"></div>
    <Tabbtn></Tabbtn>
  </div>
</template>

<script>
// @ is an alias to /src

import axios from "axios";
import api from "../assets/config/api";
import Tabbtn from '@/components/Tabbtn.vue'

import Vue from "vue";
import { Lazyload } from "vant";
Vue.use(Lazyload);

export default {
  name: "Home",
  data() {
    return {
      serchData: "",
      data: {},
      tabbarActive: 0,
    };
  },
  computed: {
    images: function () {
      if (typeof this.data.banner == "object") {
        return this.data.banner;
      } else {
        return [];
      }
    },
    channel() {
      if (typeof this.data.channel == "object") {
        return this.data.channel;
      } else {
        return [];
      }
    },
    brandList() {
      if (typeof this.data.brandList == "object") {
        return this.data.brandList;
      } else {
        return [];
      }
    },
    newGoodsList() {
      if (typeof this.data.newGoodsList == "object") {
        return this.data.newGoodsList;
      } else {
        return [];
      }
    },
    hotGoodsList() {
      if (typeof this.data.hotGoodsList == "object") {
        return this.data.hotGoodsList;
      } else {
        return [];
      }
    },
  },
  components: {
    Tabbtn
  },
  async mounted() {
    // console.log(api)
    let res = await axios.get(api.IndexUrl);
    this.data = res.data.data;
    console.log(this.data);
  },
};
</script>
<style lang="less">
* {
  margin: 0;
  padding: 0;
}
.home {
  .swiperimg {
    width: 375px;
    height: 200px;
  }
}
.brandList {
  .van-grid-item__content {
    padding: 0;
  }
  .van-image {
    border: 2px solid #fff;
  }
  .title {
    position: absolute;
    top: 20px;
    left: 5px;
  }
  .price {
    position: absolute;
    top: 40px;
    left: 5px;
    font-size: 10px;
    color: #999;
  }
}
.newGoodsList {
  .van-image {
    border: px solid #fff;
  }
  .van-grid-item__content {
    padding: 0;
  }
  .van-image {
    border: 1px solid #fff;
  }
  .price {
    font-size: 10px;
    color: #999;
  }
}

.hotGoodsList {
  .van-card__content {
    justify-content: center;
    text-align: left;
    .van-card__title {
      font-size: 14px;
      font-weight: 900;
      color: #333;
      padding: 5px 0;
    }
    .van-card__price {
      color: red;
    }
  }
}
</style>

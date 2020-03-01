<template>
    <div>
      <p>下記が購入リストになります。</p>
      <button @click="openModal">選択</button>
      <div id="overlay" v-show="showContent">
        <div id="content">
          <p>下記より購入する商品を入力してください</p>
          <select v-model="selected">
            <option disabled value="">選択してください</option>
            <option v-for="option in options" :value="option.price" :key="option.name">
              {{option.name}}
            </option>
          </select>
          ：<input type="number" :value="" min="0">
          <div class="container-inline">
            <p><button @click="cloesModal">購入</button></p>
          </div>

        </div>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      selected:"",
      options:[
        {
          name:'りんご',
          price:'300',
          quantity:0,
        },
        {
          name:'れもん',
          price:'1000',
          quantity:0,
          },
        {
          name:'もも',
          price:'500',
          quantity:0,
          },
      ],
      showContent: false,
      quantity:0,
      buyitem:"",
    }
  },
  methods:{
    openModal: function(){
      this.showContent = true;
    },
    cloesModal: function(){
      this.showContent = false;
    }
  }
}
</script>

<style scoped>
#overlay{
  z-index: 1;

  position:fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  background-color:rgba(0,0,0,0.5);

  display: flex;
  align-items: center;
  justify-content: center;
}

#content{
  z-index:2;
  width:50%;
  padding:1em;
  background:#fff;
}
</style>
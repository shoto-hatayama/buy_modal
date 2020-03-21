<template>
    <div>
      <button @click="openModal">選択</button>
      <button v-show="showBuyBtn" @click="buy">購入</button>
      <p>下記が購入リストになります。</p>
      <div v-for="(buyItem, index) in buyItems" :key="buyItem.name">
        {{buyItem.name}} {{buyItem.price}}円 ×{{buyItem.quantity}} ={{totalPrice(buyItem.price,buyItem.quantity)}} <button @click="buyDelete(index)">取り消し</button>
      </div>

      <div id="overlay" v-show="showContent">
        <div id="content">
          <p>下記より購入する商品を入力してください</p>
          <select v-model="selected">
            <option disabled value="">選択してください</option>
            <option v-for="option in options" :value="option" :key="option.name">
              {{option.name}}
            </option>
          </select>
          ：<input v-model="quantity" type="number" min="0">
          <div class="container-inline">
            <p>
              <button @click="itemBuy">購入</button>
              <button @click="closeModal">閉じる</button>
            </p>
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
      quantity:0,
      options:[
        {
          id:1,
          name:'りんご',
          price:'300'
        },
        {
          id:2,
          name:'れもん',
          price:'1000'
          },
        {
          id:3,
          name:'もも',
          price:'500'
          },
      ],
      showContent: false,
      buyItems:[],
    }
  },
  computed:{
    showBuyBtn (){
      return !!this.buyItems.length;
    },
    totalPrice (){
        return function(price,quantity){
          return price*quantity;
        }
    }
  },
  methods:{
    openModal (){
      this.showContent = true;
    },
    closeModal: function(){
      this.showContent = false;
      this.selected="";
      this.quantity=0;
    },
    itemBuy (){
      if(this.quantity != 0 && this.selected != ""){
        let item_search = this.buyItems.find(item => item.name == this.selected.name);
        if(!!item_search){
          item_search.quantity = parseInt(item_search.quantity) + parseInt(this.quantity);
        }else{
          this.buyItems.push(
            {name:this.selected.name,
            price:this.selected.price,
            quantity:this.quantity
            });
        }
        this.selected="";
        this.quantity=0;
      }
    },
    buy (){
      alert("購入しました。");
      this.buyItems=[];
    },
    buyDelete (index){
      this.buyItems.splice(index,1);
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
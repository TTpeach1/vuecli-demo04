<template>
  <div>
    <div>
        <table>
            <tr>
                <th>
                    <input type="checkbox" v-model="isAll">
                    <span>全选</span>
                </th>
                <th>商品</th>
                <th>单价</th>
                <th>数量</th>
                <th>小计</th>
                <th>操作</th>
            </tr>
            <tr v-for="(item,index) in arr" :key="index">
                <td>
                    <input type="checkbox" v-model="item.c">
                </td>
                <td>{{item.name}}</td>
                <td>{{item.price}}</td>
                <td>
                    <button :disabled='item.num<=0' @click="item.num--">-</button>
                    {{item.num}}
                    <button @click="item.num++">+</button>
                </td>
                <td>{{item.num*item.price}}</td>
                <td>
                    <button @click="del(item.name)">删除</button>
                </td>
            </tr>
        </table>
    </div>
    <div class='foot'>
        <div class="left">
            <button @click="delChange">删除选中的商品</button>
            <button @click="delAll">清空购物车</button>
        </div>
        <div class="right">
            <span>已选中{{newNum}}件商品</span>
            <span>总价：￥{{newSum}}</span>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            arr:[
                {name:'儿童书籍',price:66,num:0,sum:0,c:false},
                {name:'青年书籍',price:44,num:0,sum:0,c:false},
                {name:'成人书籍',price:88,num:0,sum:0,c:false},
            ]
        }
    },
    methods:{
        del(val){
            const index = this.arr.findIndex((item)=>{
                return val==item.name
            })
            console.log(index);
            this.arr.splice(index, 1);
        },
        delAll(){
            this.arr.splice(0,this.arr.length)
        },
        delChange(){
            const newArr = this.arr.filter((ele)=>{
                return ele.c==false;
            })
            console.log(newArr);
            return this.arr=newArr
        },
    },
    
    computed:{
        isAll:{
            set(val){
                this.arr.forEach((ele)=>ele.c=val)
            },
            get(){
                return this.arr.every(ele=>ele.c)
            }
        },
        newNum(){
            const newArr1=this.arr.filter((ele)=>{
                return ele.c==true;
            })
            return newArr1.reduce((sum,val)=>{
                return sum+=val.num
            },0)
        },
        newSum(){
            const newArr2=this.arr.filter((ele)=>{
                return ele.c==true;
            })
            return newArr2.reduce((sum,val)=>{
                return sum+=val.num*val.price
            },0)
        }
    }
}
</script>

<style>
 table{
    border-collapse: collapse;
    margin: 0 auto;
    text-align: center;
 }
 table td,table th{
    border:1px solid #cad9ea;
    color: #666;
    width: 100px;
    height:40px;
 }
 .foot{
    display: flex;
    justify-content:center;
 }
 
</style>
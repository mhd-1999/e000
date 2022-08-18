<template>
    <div id="input-search">
        <input type="text" v-model.lazy="searchValue" :placeholder="placeHolder">
        <!-- <li v-for="point in points" :key="point.code">
            {{ point.name }}
        </li> -->
        <div class="list">
            <li v-for="point in pointList" :key="point.code" @click="pointArr.push(point.name)">
                {{point.name}}
            </li>
        </div>
        <button v-for="(point,index) in pointArr" :key="index" @click="deletePoint(index)">{{point}}</button>
    </div>
</template>

<script>
import axios from "axios";
export default {
    name:"InputSearch",
    props:{
        placeHolder:String,
    },
    data(){
        return{
            searchValue:'',
            points:[],
            pointArr:[],
        }
    },
    methods:{
        deletePoint(index){
            this.points.pop(index)
        }
        
    },
    created(){
       axios.get('https://provinces.open-api.vn/api/')
       .then(res=>{
        this.points = res.data;
       })
    },
    computed:{
        pointList(){
            console.log('change');
            
            return this.points.filter((point)=>point.name.toLowerCase().match(this.searchValue.toLowerCase()));
        }
    }
}
</script>

<style scoped>
    #input-search{
        padding-top: 168px;
    }
    #input-search input{
        width: 400px;
        padding: 14.5px 10px;
        border: 1px solid #DBDBDB;
        border-radius: 4px;
        font-size: 14px;
        background: rgba(230, 249, 255, 0.2);
    }
    #input-search input:focus{
        outline: none;
        border:1px solid #1991D2 !important;
    }
    #input-search .list{
        display: flex;
        
        justify-content: center;
        flex-wrap: wrap;
        width: 400px;
        list-style: none;
        background: #F1F5F8;
    }
    .list li{
        width: 100%;
        padding: 8px 0 8px 10px;
        font-size: 16px;
        line-height: 23px;
        color: #486581;
        align-items: flex-start;
    }
</style>
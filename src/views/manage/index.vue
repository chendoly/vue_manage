<template>
  <div class="manage tc">
      <button v-on:click="add">新增</button>
      <div class="input-area" v-show="showAdd">
        <input type="text" placeholder="请输入人员姓名" v-model="nameValue" >
        <button v-on:click="addName">确定</button>
      </div>
    <table class="table">
      <tr>
        <th class="table_first_col">姓名</th>
        <th>操作</th>
      </tr>
      <tr v-for="(item,index) in peoples">
        <td class="table_first_col">{{item.name}}</td>
        <td v-bind:id="index"><span v-on:click="edit">编辑</span><span v-on:click="del">删除</span></td>
      </tr>
    </table>
      <div class="wrap" v-show="showEdit">
        <div class="content">
          <input type="text" placeholder="请输入新姓名" v-model="newName">
          <button v-on:click="cancel">取消</button>
          <button v-on:click="editName">确认</button>
        </div>  
      </div>
    <footer-nav v-bind:class="{'isManage':isNowPage}"></footer-nav>
  </div>
</template>

<style>
.manage button:first-child{width: 216px;height: 45px;background-color: #55b983;border-radius: 4px;}
.input-area{margin-top: 20px;margin-bottom: 50px;}
.input-area button{width: 66px;height: 42px;background-color: #55b983;border-radius: 4px;}
.input-area input{width: 216px;height: 42px;border:1px solid #767676}
.table{width: 100%;margin-top: 20px;}
.table span{display: inline-block;padding: 0 2px}
.table .table_first_col{width: 50%}
.wrap{display: table;background: rgba(0,0,0, 0.8);height: 100%;width: 100%;;z-index: 10;position: fixed;top: 0;left: 0;}
.wrap .content{display: table-cell;vertical-align: middle}
.wrap .content input{height: 40px; line-height: 40px; display:block; margin:0 auto; margin-bottom:10px; font-size:16px;}
.wrap .content button{width:100px; height: 30px; line-height: 30px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
</style>


<script>
import FooterNav from "../../components/footer.vue";
export default {
    components:{
      FooterNav
    },
    data:function(){
      return{
        isNowPage:true,
        showAdd:false,
        showEdit:false,
        peoples:[{'name':'Jack'},{'name':'Joe'}],
        nameValue:'',
        newName:'',
        editId:0
      }
    },
    methods:{
      add:function(){
          this.showAdd = !this.showAdd
      },
      addName:function(){ //新增人员
        var v = this.nameValue;
        if(v.trim() ==""){
          alert("请输入新增人员姓名")
        }else{
          var data={}
          data.name = v;
          this.peoples.push(data);
          this.nameValue=""
        }
      },
      del:function(e){ //删除人员
        var id = e.target.offsetParent.id;
        this.peoples.splice(id,1)
      },
      edit:function(e){ //编辑人员
        var id = e.target.offsetParent.id;
        this.showEdit = true;
        this.editId = id;
        this.newName = this.peoples[id].name;
      },
      cancel:function(){ //取消编辑
        this.showEdit = false
      },
      editName:function(){ //修改名字
        var v = this.newName;
        if(v.trim()==""){
          alert("请输入姓名")
        }else{
          this.peoples[this.editId].name = this.newName;
          this.showEdit = false;
        }
      }
    }
}
</script>

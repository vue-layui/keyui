<template>
  <div class="AppTable">
        <div class="panel PanelLine">            
            <table class="Table Line" border="1" cellspacing="0" style="width: 100%;">
                <thead>
                    <tr>
                        <th>序号</th>
                        <th>用户名</th>
                        <th>年龄</th>
                        <th>毕业学校</th>
                        <th>操作</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(person,index) in people" :key=index :index='index'>
                        <td>{{index+1}}</td>
                        <td>{{person.name}}</td>
                        <td>{{person.age}}</td>
                        <td>{{person.school}}</td>
                        <td><button @click="deletePerson(index)">remove</button></td>
                    </tr>
                    <tr class="lastr">
                        <td></td>
                        <td><input type="text"  id="name" v-model="newPerson.name"/></td>
                        <td><input type="text" id="age" v-model="newPerson.age"/></td>
                        <td><input type="text" id="school" v-model="newPerson.school"/></td>
                        <td><button @click="createPerson">insert</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TableOne',     
    data () {
        return {
          newPerson: {  
              index:'',              
              name: '',  
              age: 0,  
              school: ''  
          },
          people: [
              {                       
                  name: '王明',  
                  age: 22,  
                  school: '清华大学'  
              },
              {  
                  name: '李磊',  
                  age: 21,  
                  school: '复旦大学'  
              },
              {  
                  name: '陈晨',  
                  age: 19,  
                  school: '交通大学'  
              },
          ]
        }
      },
    methods:{  
          createPerson(){  
              this.people.push(this.newPerson);  
              // 添加完newPerson对象后，重置newPerson对象  
              this.newPerson = {index:'',name: '', age: 0, school: ''}  
          },  
          deletePerson(index){  
              // 删一个数组元素  
              this.people.splice(index,1);  
          }  
      }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Line{
    border: 1px solid #ddd;
}
</style>
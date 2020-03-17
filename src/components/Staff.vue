<template>
    <div class="staff">
        <b-button class="btn btn-info add_staff_button" @click="addEmployee($bvModal)">Добавить сотрудника</b-button>

        <table class="table table-bordered">
             <thead>
               <tr>
                    <th>#ID</th>
                    <th>ФИО</th>
                    <th>Контакты</th>
                    <th>Действия</th>
               </tr>
             </thead>
             <tbody>
             <tr v-for="item in items" :key="item.id">
                  <td>{{ item.id}}</td>
                  <td>{{ item.name }}</td>
                  <td>{{ item.email }}</td>
                  <td>
                      <a href="#" @click="editEmployee($bvModal, item)"><font-awesome-icon :icon="['fas', 'user-edit']" /></a>&nbsp;
                      <a href="#" @click="deleteEmployee(item)"><font-awesome-icon :icon="['fas', 'trash']" /></a>
                  </td>
             </tr>
             </tbody>
        </table>

        <StaffModal :item="item" v-on:change="changeHandler($event)" />
    </div>
</template>

<script>
   // import axios from 'axios';
    import StaffModal from "./StaffModal";

    export default {
        name: "Staff",
        components: {StaffModal},
        data: function() {
            return {
               item: false,
               items: [
                   {id: 1, name: "Иванов Иван Иванович", email: "i.ivanov@gmail.com"},
                   {id: 2, name: "Иванова Нина Сергеевна", email: "n.ivanova@gmail.com"},
               ]
        };
      },
      mounted() {
          /*  axios.get('http://laravel.test/api/staff')
              .then((response) => {
                  this.items = response.data;
                  console.log(response);
              })
              .catch((error) => {
                  console.log(error);
              }); */
      },
      methods: {
         addEmployee(modal) {
             this.item = false;
             modal.show('staff_modal');
         },
         editEmployee(modal, item) {
            this.item = item;
            modal.show('staff_modal');
         },
         deleteEmployee(item) {
             if(confirm("Уверены, что хотите удалить работника?")) {
                 for(let i = 0; i < this.items.length; i++) {
                     if(this.items[i].id != item.id) continue;
                     this.items.splice(i, 1);
                     /*axios.delete('http://laravel.test/api/staff/' + item.id, {})
                          .then((response) => {
                              console.log(response);
                          })
                          .catch((error) => {
                              console.log(error);
                          }); */
                 }
             }
         },
         changeHandler(e){
             let id = e.id;
             if(!id) {
                 id = this.items.length + 1;
                 let request = {id:id, name:e.name, email:e.email};
                 this.items.push(request);
                 /*axios.post('http://laravel.test/api/staff', request)
                      .then((response) => {
                          console.log(response);
                      })
                      .catch((error)  => {
                          console.log(error);
                      });*/
             }else{
                 for(let i = 0; i < this.items.length; i++) {
                     if(this.items[i].id != id) continue;
                     this.items[i].name  = e.name;
                     this.items[i].email = e.email;


                    /* axios.put('http://laravel.test/api/staff/' + id, {name: e.name, email: e.email}, )
                         .then((response) => {
                             console.log(response);
                         })
                         .catch((error)  => {
                             console.log(error);
                         });*/
                 }
             }

         }
      }
    }
</script>

<style scoped>

</style>
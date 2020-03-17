<template>
    <div>
            <b-modal
                    id="staff_modal"
                    ref="modal"
                    :title="item ? 'Редактировать работника' : 'Новый работник'"
                    @show="resetModal"
                    @hidden="resetModal"
                    @ok="handleOk"
            >
                <form ref="form" @submit.stop.prevent="handleSubmit">
                <b-form-group
                        :state="nameState"
                        label="ФИО работника"
                        label-for="name-input"
                        invalid-feedback="Name is required"
                >
                <b-form-input class="form-control"  v-model="name"
                              :state="nameState" id="name-input"
                              required placeholder="ФИО работника" ></b-form-input>
                </b-form-group>

                    <b-form-group
                            :state="emailState"
                            label="E-mail работника"
                            label-for="email-input"
                            invalid-feedback="E-mail is required"
                    >
                    <b-form-input class="form-control" v-model="email"
                                  :state="emailState" id="email-input"
                                  required
                                  placeholder="E-mail работника"></b-form-input>
                    </b-form-group>
            </form>
        </b-modal>

    </div>
</template>

<script>
    export default {
        name: "StaffModal",
        props: ['item'],
        data() {
            return {
                nameData: '',
                emailData: '',
                nameState: null,
                emailState: null
            }
        },
        computed: {
            name : {
                get : function() {
                    return this.item.name;
                },
                set: function(newName) {
                        this.nameData = newName;
                      //  this.item.name = newName;

                }
            },
            email: {
                get : function() {
                    return this.item.email;
                },
                set: function (newEmail) {
                        this.emailData = newEmail;
                        //this.item.email = newEmail;

                }
            }
        },
        methods: {
            checkFormValidity() {
                const valid = this.$refs.form.checkValidity();
                this.nameState  = valid;
                this.emailState = valid;
                return valid;
            },
            resetModal() {
                this.nameState = null;
                this.emailState = null;
            },

            handleOk(e){
                e.preventDefault();
                this.handleSubmit();
            },
            handleSubmit(){
                //Выходим, если форма не валидна
                if (!this.checkFormValidity()) {
                    return;
                }
                //добавляем или изменяем данные в items
                let itemElement = this.$props.item;
                let data = { name: this.nameData, email: this.emailData };
                if(itemElement) {
                    data.id = itemElement.id;
                    if(!data.name)  data.name = itemElement.name;
                    if(!data.email) data.email = itemElement.email;
                }
               console.log(data);
                this.$emit('change', data);

                //Закрываем окно
                this.$nextTick(() => {
                    this.$bvModal.hide('staff_modal')
                });
            }

        }
    }
</script>

<style scoped>

</style>
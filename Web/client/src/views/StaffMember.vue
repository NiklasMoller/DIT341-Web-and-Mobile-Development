<template>
  <div>
    <br>
    <h3>Staff Member</h3>

    <div class="createForm">
      <b-form @submit="onSubmit">

      <b-form-group id="input-group-1" label="Name" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="form.staffmemberName"
            required
            :placeholder=" form.staffmemberName "
          ></b-form-input>
      </b-form-group>
<br>
        <b-form-group id="input-group-2" label="Salary per hour" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.staffSalary"
            required
            :placeholder="form.staffSalary"
          ></b-form-input>
        </b-form-group>
<br>
        <b-form-group id="input-group-3" label="E-mail" label-for="input-3">
          <b-form-input
            id="input-3"
            v-model="form.staffEmail"
            type="email"
            required
            :placeholder=" form.staffEmail "
          ></b-form-input>
        </b-form-group>

        <br>
        <b-button type="submit" variant="danger">Update Staffmember
          <router-link :to="{path: '/staffMembers'}">
          </router-link></b-button>



        <b-button variant="info" id="b-button" href="/staffmembers">
          Back to staffmembers
          </b-button>

      </b-form>
      
    </div>

  </div>
</template>

<script>
    import { Api } from '@/Api'


    export default {
        name: 'Project',
        data() {
            return {

              form: {
                staffmemberName: '',
                staffSalary: '',
                staffEmail: '',
              },
                show: true
            }
        },
        mounted() {
            this.getStaffmember();

        },
        methods: {
          onSubmit(evt) {
            evt.preventDefault()
            //alert(JSON.stringify(this.form))
            console.log(this.form.staffmemberName);

            Api.put(`/staffMembers/${this.$route.params.id}`, {
              name: this.form.staffmemberName,
              salaryPerHour: this.form.staffSalary,
              email: this.form.staffEmail
            })
              .then(function (response) {
                console.log(response);
                alert("Sucessfully updated the staff member!")
              })
              .catch(function (error) {
                console.log(error);
              });
          },
            getStaffmember() {
                Api.get(`/StaffMembers/${this.$route.params.id}`)
                    .then(response => {
                        this.form.staffmemberName = response.data.name
                        this.form.staffSalary = new String(response.data.salaryPerHour); //casting to String for input field
                        this.form.staffEmail = response.data.email

                    })
                    .catch(error => {
                        console.log(error)
                    })
            }
        }
    }







</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import '/../assets/css/stylesheet.css';

  #b-button {
    margin-left: 10px;
  }
</style>

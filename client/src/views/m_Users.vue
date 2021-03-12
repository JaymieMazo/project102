<template>


<v-card>

<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            Calories
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in users"
          :key="item.UserCode"
        >
          <td>{{ item.UserCode }}</td>
          <td>{{ item.Password }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
   </v-card>
</template>






<script>
import axios from "axios"
export default {
    data() {
        return {
            users:[],
            sortdesc: false,
            singleselect: false,
            userDialog: false,
            chkuserlvl: false,
            drawer:false,
            btnadd_user: '',
            btnedit_user: '',
            btndelete_user: '', 
          
            search: '',
            selected: [],
            sortby: 'uname',
            loadData: [{
                uname: 'test',
                pword: 'test',
                userlvl: 0,
                updateddate: '',
                updatedby: '',

            }],

            keys: [
                'Username',
                'Password',
                'Userlevel',
                'UpdatedDate',
                'UpdatedBy'
            ],
            
            headers: [{
                    text: 'Username',
                    value: 'uname',
                    align: 'start',
                    sortable: false
                },

                {
                    text: 'Password',
                    value: 'pword'
                },
                {
                    text: 'User level',
                    value: 'userlvl'
                },
                {
                    text: 'Updated Date',
                    value: 'updateddate'
                },
                {
                    text: 'UpdatedBy',
                    value: 'updatedby'
                }
            ],
            userLevel:[],

            NavItems:[
                        {title:'Home' , icon: 'mdi-view-dashboard'},
                        {title:'User Accounts' ,icon: 'mdi-account-lock'},
                        {title:'Employees' , icon: 'mdi-account-group'}, 
                        {title: 'Departments', icon: 'mdi-bank'} ,
                          {title: 'Sections', icon: 'mdi-bank-minus'} ,
                        {title: 'Status', icon: 'mdi-graph'} ,
                        {title: 'Programming Language', icon: 'mdi-language-javascript'}        
                ]
        }
    },


    created() {
        this.mUsers()
    },
    


    methods: {
        mUsers() {
            let url = this.api + `/m_Users`
            axios.get(url).then(res => {
                this.users=res.data
                    console.log(res.data)
                    // this.loadData.splice(0)
                    // let data = res.data
                    // for (let x = 0; x < data.length; x++) {
                    //     // this.deserts.push(data[x]);
                    //     this.loadData.push({
                    //         uname: data[x].UserCode,
                    //         pword: data[x].Password,
                    //         userlvl: data[x].UserlevelID,
                    //         updateddate: data[x].UpdatedDate,
                    //         updatedby: data[x].UpdatedByCode,
                    //     });
                    // }

                })
                .catch(err => {
                    console.log(err)
                })
        },



        mUserLevels() {
            let url = this.api + `/m_UserLevels`
            axios.get(url)
                .then(res => {
                    this.userLevel = res.data
                    console.log(this.userLevel)
                })
        },

    },
}
</script>
 
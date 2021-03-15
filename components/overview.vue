<template>
  <div>
    <v-btn color="primary" dark @click="openModal()">
      Open Modal
    </v-btn>
    <v-row align="center" no-gutters style="height:25px;"> </v-row>

    <Add
      :openModal="modalvalue"
      @closeModal="modalvalue = false"
      @saveItem="save"

    />
    <Edit
      :openModal="editModal"
      :item="editArray"
      @closeModal="editModal = false"
      @edit="edit"
    />

    <v-simple-table>
      <thead>
        <tr>
          <th class="text-left">
            First Name
          </th>
          <th class="text-left">
            Last Name
          </th>
        </tr>

        <tr v-for="(item, i) in itemObject" :key="i">
          <td>{{ item.firstName}}</td>
          <td>{{ item.lastName }}</td>

          <td>
            <v-btn class="mx-2" fab dark small color="primary" @click="editMethod(item)">
              <v-icon dark>
                mdi-pencil
              </v-icon>
            </v-btn>
          </td>
        </tr>
      </thead>
    </v-simple-table>
  </div>
</template>

<script>
import Add from "@/components/Add.vue";
import Edit from "@/components/edit.vue";
import { makeId } from "@/utilities/makeId";
export default {
  components: {
    Add,
    Edit
  },
  data() {
    return {
      modalvalue: false,
      editModal: false,
      itemObject: [],
      editArray : []
    };
  },

  methods: {
    openModal() {
      this.modalvalue = true;
    },
    save(value) {
      this.itemObject.push({
        id: makeId(50),
        firstName: value.firstName,
        lastName: value.lastName 
      });
      this.modalvalue = false;
    },
    editMethod(item) {
      this.editModal = true;
      this.editArray = {...item};
    },
    edit(value){
      this.editArray = [];
      const index = this.itemObject.findIndex(item => item.id === value.id); 
      this.itemObject.splice(index,1,value);
      this.editModal = false;
    }
  }
};
</script>

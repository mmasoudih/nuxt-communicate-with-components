<template>
  <div>
    <v-btn color="primary" dark @click="openModal()">
      Open Modal
    </v-btn>
    <v-row :align="align" no-gutters style="height:25px;"> </v-row>

    <Add
      :openModal="modalvalue"
      @closeModal="modalvalue = false"
      :itemArray="itemArray"
      :itemObject="itemObject"
      @saveItem="save($event)"
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

        <tr v-for="(itemObject, i) in itemArray" :key="i">
          <td>{{ itemObject.FirstName }}</td>
          <td>{{ itemObject.LastName }}</td>

          <td>
            <v-btn class="mx-2" fab dark small color="primary" @click="editMethod(itemObject)">
              <v-icon dark>
                mdi-pencil
              </v-icon>
            </v-btn>
          </td>
          <Edit
            :openModal="modalvalue"
            @closeModal="modalvalue = false"
            :itemArray="itemArray"
            :itemObject="itemObject"
            @edit="edit($event)"
          />
        </tr>
      </thead>
    </v-simple-table>
  </div>
</template>

<script>
import Add from "@/components/Add.vue";
import Edit from "@/components/edit.vue";

export default {
  components: {
    Add,
    Edit
  },
  data() {
    return {
      modalvalue: false,

      itemArray: [],
      itemObject: { FirstName: "", LastName: "" }
    };
  },

  methods: {
    openModal() {
      this.modalvalue = true;
      
    },
    save() {
      this.itemArray.push(this.itemObject);
      this.itemObject = {};

      this.modalvalue = false;
    },
    editMethod(itemObject) {
      this.itemObject = itemObject;
      this.modalvalue = true;
    }
  }
};
</script>

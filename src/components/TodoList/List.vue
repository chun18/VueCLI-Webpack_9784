<template>
 <v-main class="list">
   <h3 class="text-h3 font-weight-medium mb-5">To Do List</h3>

   <v-card>
     <v-card-title>
       <v-text-field
         v-model="search"
         append-icon="mdi-magnify"
         label="Search"
         single-line
         hide-details
       ></v-text-field>
       <v-container fluid>
    <v-row align="center">
      <v-col
        class="d-flex"
        cols="12"
        sm="6"
        <v-select
          :items="['Penting', 'Biasa', 'Tidak penting']"
          label="All Priority"
          outlined>
        </v-select>
      </v-col>
       </v-row>
  </v-container>
       <v-spacer></v-spacer>
       <v-btn color="success" dark @click="dialog = true">
         Tambah
       </v-btn>
     </v-card-title>
     <v-data-table :headers="headers" :items="todos" :search="search">
       <template v-slot:[`item.actions`]="{ item }">
         <v-btn small class="mr-2" @click="dialog1 = true">
           edit
         </v-btn>
         <v-btn small @click="dialog2 = true">
           delete
         </v-btn>
       </template>
     </v-data-table>
   </v-card>

   <v-dialog v-model="dialog" persistent max-width="600px">
     <v-card>
       <v-card-title>
         <span class="headline">Form Todo</span>
       </v-card-title>
       <v-card-text>
         <v-container>
           <v-text-field
             v-model="formTodo.task"
             label="Task"
             required
           ></v-text-field>

           <v-select
             v-model="formTodo.priority"
             :items="['Penting', 'Biasa', 'Tidak penting']"
             label="Priority"
             required
           ></v-select>

           <v-textarea
             v-model="formTodo.note"
             label="Note"
             required
           ></v-textarea>
         </v-container>
       </v-card-text>
       <v-card-actions>
         <v-spacer></v-spacer>
         <v-btn color="blue darken-1" text @click="cancel">
           Cancel
         </v-btn>
         <v-btn color="blue darken-1" text @click="save">
           Save
         </v-btn>
       </v-card-actions>
     </v-card>
   </v-dialog>

   <v-dialog v-model="dialog1" persistent max-width="600px">
     <v-card>
       <v-card-title>
         <span class="headline">Form Todo For Edit</span>
       </v-card-title>
       <v-card-text>
         <v-container>
           <v-text-field
             v-model="formTodo.task"
             label="Task"
             required
           ></v-text-field>

           <v-select
             v-model="formTodo.priority"
             :items="['Penting', 'Biasa', 'Tidak penting']"
             label="Priority"
             required
           ></v-select>

           <v-textarea
             v-model="formTodo.note"
             label="Note"
             required
           ></v-textarea>
         </v-container>
       </v-card-text>
       <v-card-actions>
         <v-spacer></v-spacer>
         <v-btn color="blue darken-1" text @click="cancel1">
           Cancel
         </v-btn>
         <v-btn color="blue darken-1" text @click="save1">
           Save
         </v-btn>
       </v-card-actions>
     </v-card>
   </v-dialog>

   <v-dialog v-model="dialog2" max-width="290">
      <v-card>
        <v-card-title class="headline">
         Hapus Data
        </v-card-title>

        <v-card-text>
         Yakin mau Hapus???
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            color="green darken-1"
            Tidak
            @click="dialog = false"
          >
            Disagree
          </v-btn>

          <v-btn
            color="green darken-1"
            Ya
            @click="dialog = false"
          >
            Agree
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
 </v-main>
</template>
<script>
export default {
 name: "List",
 data() {
   return {
     search: null,
     dialog: false,
     dialog1: false,
     dialog2: false,
     headers: [
       {
         text: "Task",
         align: "start",
         sortable: true,
         value: "task",
       },
       { text: "Priority", value: "priority" },
       { text: "Note", value: "note" },
       { text: "Actions", value: "actions" },
     ],
     todos: [
       {
         task: "bernafas",
         priority: "Penting",
         note: "huffttt",
       },
       {
         task: "nongkrong",
         priority: "Tidak penting",
         note: "bersama tman2",
       },
       {
         task: "masak",
         priority: "Biasa",
         note: "masak air 500ml",
       },
     ],
     formTodo: {
       task: null,
       priority: null,
       note: null,
     },
   };
 },
 methods: {
   save() {
     this.todos.push(this.formTodo);
     this.resetForm();
     this.dialog = false;
   },
   save1() {
     this.todos.push(this.formTodo);
     this.resetForm1();
     this.dialog1 = false;
   },
   cancel() {
     this.resetForm();
     this.dialog = false;
   },
   cancel1() {
     this.resetForm1();
     this.dialog1 = false;
   },
    resetForm1() {
     this.formTodo = {
       task: null,
       priority: null,
       note: null,
     };
   },
   resetForm() {
     this.formTodo = {
       task: null,
       priority: null,
       note: null,
     };
   },
 },
};
</script>

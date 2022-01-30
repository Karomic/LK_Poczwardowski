<template>
   <div class="editModal">
      <h1 class="title is-4 margin0">Editing: "{{ row.name }}"</h1>
      <div class="editCells">
         <div class="labels">
            <label for="name" class="is-size-5">Name:</label>
            <label for="status" class="is-size-5">Status:</label>
         </div>
         <div class="inputs">
            <input
               type="text"
               class="input is-info is-small"
               id="name"
               v-model="name"
               :placeholder="row.name"
            />
            <select
               name="status"
               class="select is-link is-small"
               id="status"
               v-model="status"
            >
               <option v-for="item in items" :value="item.val" :key="item.id">
                  {{ item.val }}
               </option>
            </select>
         </div>
      </div>
      <div class="buttons">
         <button
            class="save button is-link margin0"
            @click="
               saveAndClose({ name: name, status: status, id: this.row.id })
            "
         >
            <span>Save</span>
         </button>
         <button class="discard button is-danger margin0" @click="close">
            <span>Discard</span>
         </button>
      </div>
   </div>
</template>

<script>
export default {
   name: 'Edit',
   methods: {
      close() {
         this.$emit('close')
      },
      saveAndClose(savedData) {
         this.$emit('save', savedData)
         this.name = ''
         this.status = ''
         this.close()
      }
   },
   props: {
      row: {
         type: Object
      }
   },
   data() {
      return {
         name: this.row.name,
         status: this.status,
         row1: this.row,
         items: [
            { id: 1, val: 'verified' },
            { id: 2, val: 'unverified' }
         ]
      }
   }
}
</script>

<style lang="scss" scoped>
.editModal {
   background: $modal-background-background-color;
   border: $primary solid 4px;
   border-radius: $radius;
   position: absolute;
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: space-evenly;
   width: 445px;
   height: 275px;
   top: 35vh;
   left: 35vw;
   backdrop-filter: blur(2px);

   h1 {
      width: 100%;
   }

   .bulma-delete-mixin {
      @include delete;
   }

   .editCells {
      display: flex;
      flex-direction: row;
      justify-content: space-evenly;
      align-items: center;
      width: 80%;
      height: 120px;

      .labels {
         display: flex;
         flex-direction: column;
         justify-content: space-evenly;
         width: 40%;
         height: 100%;
      }

      .inputs {
         display: flex;
         flex-direction: column;
         justify-content: space-evenly;
         width: 50%;
         height: 100%;
         input {
            text-align: center;
            width: 100%;
         }
         select {
            text-align: center;
         }
      }
   }
   .buttons {
      display: flex;
      flex-direction: row;
      justify-content: space-around;
      align-items: center;
      width: 200px;
      height: 50px;

      .bulma-control-mixin {
         &.is-small {
            @include control-small;
         }

         &.is-medium {
            @include control-medium;
         }

         &.is-large {
            @include control-large;
         }
      }
   }

   .margin0 {
      margin: 0;
   }
}
</style>

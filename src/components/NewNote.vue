<template>
    <div class="new-note">
        <label>
            Заголовок
            <input v-model="note.title" :placeholder="note.titlePlaceholder" type="text">
        </label>
        <label>
            Текст заметки
            <textarea v-model="note.description" :placeholder="note.descriptionPlaceholder" name="" id="" cols="30" rows="10"></textarea>
        </label>
        <button class="btn btnPrimary" type="button" @click="addNote">Опубликовать</button>
    </div>
</template>


<script>
export default {
    name: "NewNote",
    props: {
        message: {
            type: String,
            required: true
        },
    },
    
    data() {
        return {
            note: {
				title: "",
				titlePlaceholder:"Введите заголовок",
				description: "",
				descriptionPlaceholder: "Текст заметки"
			},
        }
    },
    
    methods: {
        addNote() {
            if (this.note.title == "") {
                this.$emit('addNote', {message: false});
            }  else {
                this.$emit('addNote', {message: "Done", newNote: {
                    title: this.note.title,
                    description: this.note.description
                }});
                this.note.title = "";
                this.note.description = "";
            }   
            
		}
    },
}
</script>


<style lang="scss">
    .new-note {
        text-align: center
    }
</style>
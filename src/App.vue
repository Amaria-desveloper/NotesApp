<template>
	<div class="wrapper">
		<div class="wrapper-content">
			<section>
				<div class="container">
					
					<!-- message for user -->
					<message v-if="message" :message="message"></message>
					
					<!-- form for NewNote -->
					<newNote :message="message" @addNote="addNote"></newNote>

					<!-- title -->
					<div class="grid-header">
						<h1> {{ title }} </h1>
						
						<search :value="search" @search="search = $event"></search>
						
						<div class="icons">
							<button :class="{active: grid}" @click="grid = true">
								<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
							</button>
							
							<button :class="{active: !grid}" @click="grid = false">
								<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
							</button>
						</div>
					</div>
					
					<!-- notes's grid -->
					<notes :data="notesFilter" :grid="grid" @removeNote="removeNote"></notes>
				</div>
			</section>
		</div>
	</div>
</template>

<script>
import message from '@/components/Message.vue';
import newNote from '@/components/NewNote.vue';
import notes from '@/components/Notes.vue';
import search from '@/components/Search.vue';


export default {
	name: 'App',
	components: {
		message,
		newNote,
		notes,
		search
	},
	data() {
		return {
			title: 'Notes App',
			message: '',
			grid: true,
			search: "",
			notes: [
				{
					title: "First Note",
					description: "Decription for First Note",
					date: new Date().toLocaleString()
				},
				{
					title: "Second Note",
					description: "Decription for Second Note",
					date: new Date().toLocaleString()
				},
				{
					title: "Third Note",
					description: "Decription for Third Note",
					date: new Date().toLocaleString()
				}
			]
		}
	},
	
	computed: {
		notesFilter() {
			let arr = this.notes;
			let search = this.search; 
			
			if (!search) { return arr }
			
			search = search.trim().toLowerCase();
			
			arr = arr.filter(item => {
				if (item.title.toLowerCase().indexOf(search) !== -1) {
					return item
				}
			})
			
			return arr
		}
	},
	
	methods: {
		addNote(payload) {
			if (!payload.message) {
				this.message = "заполните заголовок";
				return false
			}
			
			let { title, description } = payload.newNote;
			this.notes.push({
				title,
				description,
				date: new Date().toLocaleString()
			});
		},
		
		removeNote(index) {
			this.notes.splice(index, 1);
		}
	}
}
</script>

<style lang="scss">
@import '@/assets/scss/utils/vars.scss';

.grid-header {
	display: flex;
	justify-content: space-between;
	margin-top: 40px;
	
	& .icons {
		display: flex;
		gap: 20px;
		
		& button.active {
			cursor: pointer;
			color: $primary-color;
		}
	}
}
</style>

<template>
	<div>
		<div class="fixed bottom-0 right-0 m-12">
			<button class="px-4 py-1 rounded-full shadow-lg bg-amber-500 text-white text-6xl" @click="openModal">+</button>
		</div>
		<JetDialogModal :show="modal" @close="closeModal()">
			<template #content>
				<div class="flex">
					<input type="text" name="title" id="title" class="focus:ring-amber-500 focus:border-amber-500 flex-1 block w-full rounded-l-lg sm:text-sm border-gray-300 flex-1" placeholder="Note Title" v-model="noteTitle" maxlength="20">
					<button class="p-3 rounded-r-lg shadow-lg bg-amber-500 text-white" @click="addNote()">Add</button>
				</div>
			</template>
		</JetDialogModal>
		<div class="w-full">
			<div class="flex flex-wrap mx-auto justify-center">
				<div v-for="(note, index) in notes" class="rounded-lg shadow-lg w-full md:w-1/3 m-5">
					<div class="p-4 border-b-2 border-amber-600 bg-amber-400 rounded-t-lg flex">
						<input type="text" class="outine outline-amber-600 flex-1 block w-full sm:text-sm border-none flex-1 bg-amber-400 inputLarge text-amber-900" placeholder="Note Title" v-model="notes[index]['title']" maxlength="20" @input="editTitle(note.id, notes[index]['title'])">
						<button class="text-amber-900 text-lg" @click="deleteNote(note.id)">X</button>
					</div>
					<div class="bg-amber-200 p-4">
						<textarea v-model="notes[index]['body']" class="outine outline-amber-600 border-0 w-full mb-2 bg-amber-200" ref="textareas" placeholder="" rows="10" style="resize: none;" @input="editBody(note.id, notes[index]['body'])"></textarea>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import JetDialogModal from '@/Jetstream/DialogModal.vue';
	export default {
        props: {
            user: {
                default: {}
            },
        },

        components: {
        	JetDialogModal,
        },

        data: function() {
            return {
                modal: false,
                noteTitle: null,
                notes: []
            }
        },

        methods: {
        	openModal(action){
        		this.modal = true
        	},

        	closeModal(action){
        		this.modal = false
        	},

        	addNote(){
    		  axios
                .post('api/notes', {
                  title: this.noteTitle
                })

                .then((res) => {
                	// console.log(res.data)
                  this.notes.push(res.data)
                  this.modal = false
                }).catch((err) =>{
                  console.log(err)
                })
        	},

        	editTitle(note_id, title){
        		var id = window.setTimeout(function() {}, 0);
				while (id--) {
				    window.clearTimeout(id);
				}
        		setTimeout(() => {
	    		  axios
	                .patch('api/notes/' + note_id, {
	                  title: title
	                })

	                .then((res) => {
	                	// console.log(res.data)
	                }).catch((err) =>{
	                  console.log(err)
	                })
        		}, 1000)
        	},

        	editBody(note_id, body){
    		  var id = window.setTimeout(function() {}, 0);
				while (id--) {
				    window.clearTimeout(id);
				}
        		setTimeout(() => {
	    		  axios
	                .patch('api/notes/' + note_id, {
	                  body: body
	                })

	                .then((res) => {
	                	// console.log(res.data)
	                }).catch((err) =>{
	                  console.log(err)
	                })
        		}, 1000)
        	},

        	deleteNote(id){
    		  axios
              .delete('api/notes/' + id)
              // .get('/disciplines/' + id)
              .then((res) => {
                for (var i = 0; i < this.notes.length; i++) {
                	if (this.notes[i]['id'] == id) {
                    	this.notes.splice(i, 1)
                		break
                	}
                }
              }).catch((err) =>{
                console.log(err)
              })
        	}
        },

        created: function() {
        	this.notes =  this.user.notes
        },
    }
</script>
<style type="text/css">
	input[type="text"].inputLarge
	{
	    font-size:18px;
	    font-weight: bold;
	    outline: none;
	}
</style>
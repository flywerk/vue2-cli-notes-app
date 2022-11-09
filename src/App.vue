<template>
	<div class="wrapper">
		<div class="wrapper-content">
			<section>
				<div class="container">
					<div id="app">
						<h1>{{ title }}</h1>
						<!-- warning message -->
						<message v-if="message" :message="message" />

						<newNote :note="note" @addNote="addNote" />

						<!-- note list -->
						<div class="notes">
							<div class="note" v-for="(note, index) in notes" :key="index">
								<div class="note-header">
									<p>{{ note.title }}</p>
								</div>
								<div class="note-body">
									<p>{{ note.description }}</p>
									<span> {{ note.date }} </span>
								</div>
							</div>
						</div>
					</div>
				</div>
			</section>
		</div>
	</div>
</template>

<script>
import message from "@/components/Message.vue"
import newNote from "@/components/NewNote.vue"
export default {
	components: {
		message,
		newNote,
	},
	data() {
		return {
			title: "notes app",
			message: null,
			note: {
				title: "",
				description: "",
			},
			notes: [
				{
					title: "first note",
					description: "first description",
					date: new Date(Date.now()).toLocaleString(),
				},
				{
					title: "second note",
					description: "second description",
					date: new Date(Date.now()).toLocaleString(),
				},
				{
					title: "third note",
					description: "third description",
					date: new Date(Date.now()).toLocaleString(),
				},
			],
		}
	},
	methods: {
		addNote() {
			let { title, description } = this.note

			if (title === "") {
				this.message = "title cant be blank"
				return false
			}

			this.notes.push({
				title,
				description,
				date: new Date(Date.now()).toLocaleString(),
			})
			this.message = null
			this.note.title = ""
			this.note.description = ""
		},
	},
}
</script>

<style></style>

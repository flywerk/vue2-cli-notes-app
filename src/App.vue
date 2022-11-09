<template>
	<div class="wrapper">
		<div class="wrapper-content">
			<section>
				<div class="container">
					<div id="app">
						<!-- message -->
						<message v-if="message" :message="message" />
						<!-- new note -->
						<newNote :note="note" @addNote="addNote" />
						<!-- title -->
						<div class="note-header">
							<h1>{{ title }}</h1>
							<div class="icons">
								<svg
									:class="{ active: grid }"
									@click="grid = true"
									style="cursor: pointer"
									xmlns="http://www.w3.org/2000/svg"
									width="24"
									height="24"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<rect x="3" y="3" width="7" height="7"></rect>
									<rect x="14" y="3" width="7" height="7"></rect>
									<rect x="14" y="14" width="7" height="7"></rect>
									<rect x="3" y="14" width="7" height="7"></rect>
								</svg>
								<svg
									:class="{ active: !grid }"
									@click="grid = false"
									style="cursor: pointer"
									xmlns="http://www.w3.org/2000/svg"
									width="24"
									height="24"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<line x1="8" y1="6" x2="21" y2="6"></line>
									<line x1="8" y1="12" x2="21" y2="12"></line>
									<line x1="8" y1="18" x2="21" y2="18"></line>
									<line x1="3" y1="6" x2="3" y2="6"></line>
									<line x1="3" y1="12" x2="3" y2="12"></line>
									<line x1="3" y1="18" x2="3" y2="18"></line>
								</svg>
							</div>
						</div>

						<!-- note list -->
						<notes :notes="notes" :grid="grid" @remove="removeNote" />
					</div>
				</div>
			</section>
		</div>
	</div>
</template>

<script>
import message from "@/components/Message"
import notes from "@/components/Notes"
import newNote from "@/components/NewNote"
export default {
	components: {
		message,
		notes,
		newNote,
	},
	data() {
		return {
			title: "Notes App",
			message: null,
			grid: true,
			note: {
				title: "",
				description: "",
			},
			notes: [
				{
					title: "$emit",
					description: "ponyat chto takoe $emit",
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
		removeNote(index) {
			this.notes.splice(index, 1)
		},
	},
}
</script>

<style></style>

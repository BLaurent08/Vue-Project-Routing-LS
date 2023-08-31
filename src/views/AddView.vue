<template>
    <p class="h3 text-center text-light pb-0 mb-0 mx-0 p-0 fw-semibold">Add a Tutorial</p>
    <p class="h5 text-center text-light pb-0 mb-0 mx-0 p-0 fw-semibold">After adding your tutorial be sure to visit
        tutorials and publish it!</p>
    <div class="form-group mx-0 p-0 form-floating col-12">
        <input type="text" v-model="tutorial.tutorialTitle" class="form-control rounded-5 popper" id="tutorial-title"
            placeholder="">
        <label for="tutorial-title" class="text-success-emphasis fw-semibold">Title</label>
    </div>
    <div class="form-group mx-0 p-0 form-floating col-12">
        <textarea v-model="tutorial.description" id="description" class="form-control rounded-5 popper" rows="40"
            placeholder="" style="min-height: 10rem; max-height: 40rem;"></textarea>
        <label for="description" class="text-success-emphasis fw-semibold">Description</label>
    </div>
    <button class="btn btn-outline-success rounded-pill fw-semibold text-center p-2 popper" @click="addTutorial()">Add
        Tutorial</button>
</template>

<style>
.btn-green {
    background-color: #00b800;
}

.btn-green:hover {
    background-color: #007800;
}
</style>

<script>
export default {
    data() {
        return {
            tutorial: {
                published: false,
                tutorialTitle: "",
                description: ""
            },
            tutorials: [],
            bool: true,
        }
    },
    methods: {
        addTutorial() {
            console.log("Adding tutorial...");
            if (!this.tutorial.tutorialTitle) {
                return this.$swal({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Please enter a title!',
                });
            }
            if (!this.tutorial.description) {
                return this.$swal({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Please enter a description!',
                });
            }
            this.tutorials = JSON.parse(localStorage.getItem("tutorials")) || [];
            if (this.tutorial.tutorialTitle == this.tutorials.filter(t => t.tutorialTitle == this.tutorial.tutorialTitle)[0]?.tutorialTitle) {
                return this.$swal({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Tutorial already exists!',
                });
            }
            if (this.tutorials.some(t => t.tutorialTitle == this.tutorial.tutorialTitle)) {
                return this.$swal({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Tutorial already exists!',
                });
            }
            // this.tutorials.push(this.tutorial);
            // localStorage.setItem("tutorials", JSON.stringify(this.tutorials));
            // //add ajax request here
            // axios.post("http://localhost:3000/", this.tutorial)
            //     .then((response) => {
            //         console.log(response);
            //     }, (error) => {
            //         console.log(error);
            //     });
            this.tutorial = {
                published: false,
                tutorialTitle: "",
                description: ""
            };
            this.$swal({
                icon: 'success',
                title: 'Success!',
                text: 'Tutorial added!',
            });
        },
    }
};
</script>

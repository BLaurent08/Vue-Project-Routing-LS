<template>
    <div id="search" class="input-group mx-0 p-0 rounded-pill popper">
        <div class="form-floating mx-0 p-0">
            <input type="text" v-model="search" class="form-control rounded-start-5" id="search-input" placeholder="">
            <label for="search-input" class="text-success-emphasis fw-semibold">Search</label>
        </div>
        <button class="btn text-success-emphasis btn-success rounded-end-pill fw-semibold text-center"
            @click="searchTutorial()">Search</button>
    </div>
    <table class="table table-dark table-striped table-hover mx-0 p-0 rounded-4 popper">
        <thead>
            <tr class="popper">
                <th scope="col" class="text-center">Title</th>
                <th scope="col" class="text-center">Description</th>
                <th scope="col" class="text-center">Status</th>
                <th scope="col" class="text-center">Actions</th>
            </tr>
        </thead>
        <tbody>
            <tr v-if="tutorials.length < 1">
                <td colspan="4" class="text-center">No tutorials found.</td>
            </tr>
            <tr v-for="(tutorial, index) in tutorials" :key="index">
                <td class="text-center pt-3">{{ tutorial.tutorialTitle }}</td>
                <td class="text-center">{{ tutorial.description }}</td>
                <td class="text-center pt-3">{{ tutorial.published ? "Published" : "Pending" }}</td>
                <td class="row justify-content-center align-middle">
                    <div class="btn-group-vertical">
                        <button class="btn btn-outline-success" @click="editTutorial(index)">Edit</button>
                        <button class="btn btn-outline-warning" @click="deleteTutorial(index)">Delete</button>
                    </div>
                </td>
            </tr>
        </tbody>
        <tfoot>
            <tr v-if="tutorials.length > 0">
                <td colspan="4" class="text-center border border-0"><button @click="removeAll()"
                        class="btn btn-outline-danger popper-lite">Remove All
                        Tutorials</button></td>
            </tr>
            <tr v-else>
                <td colspan="4" class="text-center border border-0">
                    <RouterLink class="btn btn-outline-success popper-lite" to="/add">Click Here to Add Some</RouterLink>
                </td>
            </tr>
        </tfoot>
    </table>
</template>

<script>
export default {
    name: "Tutorial",
    data() {
        return {
            search: "",
            tutorials: []
        }
    },
    methods: {
        deleteTutorial(index) {
            // a sweet alert to confirm the deletion
            this.$swal({
                title: 'Are you sure?',
                text: "You won't be able to revert this!",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#198754',
                cancelButtonColor: '#dc3545',
                confirmButtonText: 'Yes, delete it!'
            }).then((result) => {
                if (result.isConfirmed) {
                    this.$swal(
                        'Deleted!',
                        'Your tutorial has been deleted.',
                        'success'
                    )
                    this.tutorials.splice(index, 1);
                    localStorage.setItem("tutorials", JSON.stringify(this.tutorials));
                }
            })
        },
        searchTutorial() {
            this.tutorials = JSON.parse(localStorage.getItem("tutorials")) || [];
            if (!this.search) {
                return this.tutorials;
            }
            this.tutorials = this.tutorials.filter((tutorial) => {
                return tutorial.tutorialTitle.toLowerCase().includes(this.search.toLowerCase());
            });
        },
        editTutorial(index) {
            this.$router.push({
                name: "edit",
                params: {
                    index: index
                }
            });
        },
        removeAll() {
            //swal to confirm the deletion of all tutorials
            this.$swal({
                title: 'Are you sure?',
                text: "You won't be able to revert this!",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#198754',
                cancelButtonColor: '#dc3545',
                confirmButtonText: 'Yes, delete them all!'
            }).then((result) => {
                if (result.isConfirmed) {
                    this.$swal(
                        'Deleted!',
                        'Your tutorials have been deleted.',
                        'success'
                    )
                    this.tutorials = [];
                    localStorage.setItem("tutorials", JSON.stringify(this.tutorials));
                }
            })
        },
        // readTutorials() {
        //     axios.get("http://localhost:3000/").then((response) => {
        //         this.tutorials = response.data;
        //     }).catch((error) => {
        //         console.log(error);
        //     });
        // }
    },
    mounted() {
        // this.readTutorials();
        this.tutorials = JSON.parse(localStorage.getItem("tutorials")) || [];
    }
}
</script>
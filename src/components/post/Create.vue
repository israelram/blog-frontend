<template>
    <div>
        <div class="col-md12" form-wrapper>
            <h2> Create Post</h2>
            <form action="" id="create-post-form" @submit.prevent="createpost">
                <div class="form-group col-md-12">
                    <label for="title"> Title </label>
                    <input type="text" id="title" v-model="title" class="form-control" placeholder="Enter title">
                </div>
                <div class="form-group col-md-12">
                    <label for="description"> Description </label>
                    <input type="text" id="description" v-model="description" name="description" class="form-control" placeholder="Enter description">
                </div>
                <div class="form-group col-md-12">
                    <label for="body"> Write Content </label>
                    <textarea name="" id="body" cols="30" rows="5" v-model="body" class="form-control"></textarea>
                </div>
                <div class="form-group col-md-12">
                    <label for="autor"> Author </label>
                        <input type="text" id="author" v-model="author" name="author" class="form-control" >
                </div>
                <div class="form-group col-md-4 pull-right">
                    <button class="btn btn-success" type="submit"> Create Post </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import { server } from "../../utils/helper";
import router from "../../router";
export default {
    data() {
        return {
            title: "",
            description: "",
            body: "",
            author: "Israel Ramirez",
            date_posted: ""
        };
    },
    created() {
        this.date_posted = new Date().toLocaleDateString();
    },
    methods: {
        createPost() {
            let postData = {
                title: this.title,
                description: this.description,
                body: this.body,
                author: this.author,
                date_posted: this.date_posted
            };
            this.__submitToServer(postData);
        },
        __submitToServer(data) {
            axios.post('${server.baseURL}/blog/post', data).then(data => {
                console.log(data);
                router.push({ name: "home"});
            });
        }
    }
};
</script>
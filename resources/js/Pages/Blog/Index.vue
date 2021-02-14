<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Blog
            </h2>
        </template>
        <div>
            <div class="max-w-7xl mx-auto py-10 sm:px-6 lg:px-8">
                <div>
                    <inertia-link :href="route('blog.create')">
                        <jet-button class="bg-blue-700 text-base">Create blog</jet-button>
                    </inertia-link>
                </div>
                <table class="table-fixed">
                    <thead>
                        <tr>
                            <th class="w-3/12">Title</th>
                            <th class="w-5/12">Contents</th>
                            <th class="w-2/12">Edit</th>
                            <th class="w-2/12">Delete</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="blog in blogs" :key="blog.id">
                            <td class="border px-4 py-2">{{ blog.title }}</td>
                            <td class="border px-4 py-2">{{ blog.content }}</td>
                            <td class="border px-4 py-2 text-center">
                                <inertia-link :href="route('blog.edit', blog.id)">
                                    <jet-button class="bg-green-500 text-base">Edit</jet-button>
                                </inertia-link>
                            </td>
                            <td class="border px-4 py-2 text-center">
                                <jet-button class="bg-red-700 text-base" @click.native="deleteBlog(blog.id)">Delete</jet-button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'
    import JetButton from '@/Jetstream/Button'

    export default {
        props: ['blogs'],
        components: {
            AppLayout,
            JetButton,
        },
        data() {
            return {
                form: this.$inertia.form(
                    {
                        _method: "DELETE",
                    }
                ),
            };
        },
        methods: {
            deleteBlog(id) {
                // console.log(id);
                this.form.post(route("blog.destroy", id), {
                    preserveScroll: true,
                });
            }
        }
    }
</script>

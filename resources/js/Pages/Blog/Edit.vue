<template>
    <app-layout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Blog
            </h2>
        </template>
        <div>
            <div class="max-w-7xl mx-auto py-10 sm:px-6 lg:px-8">
                <jet-form-section @submitted="editBlog">
                    <template #title>Edit Blog</template>
                    <template #description>Edit this blog. </template>
                    <template #form>
                        <div class="col-span-6 sm:col-span-4">
                            <jet-label for="title" value="Title" />
                            <jet-input id="title" type="text" class="mt-1 block w-full" v-model="form.title" />
                            <jet-input-error :message="form.errors.title" class="mt-2" />
                        </div>
                        <div class="col-span-6 sm:col-span-4">
                            <jet-label for="content" value="Content" />
                            <textarea v-model="form.content" class="mt-1 block w-full form-input rounded-md shadow-sm"></textarea>
                            <jet-input-error :message="form.errors.content" class="mt-2" />
                        </div>
                    </template>
                    <template #actions>
                        <jet-button class="bg-blue-700">Save</jet-button>
                    </template>
                </jet-form-section>
            </div>
        </div>
    </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout';
    import JetFormSection from'@/Jetstream/FormSection';
    import JetInput from '@/Jetstream/Input';
    import JetLabel from '@/Jetstream/Label';
    import JetButton from '@/Jetstream/Button';
    import JetInputError from '@/Jetstream/InputError';

    export default {
        props: ['blog'],
        components: {
            AppLayout,
            JetFormSection,
            JetInput,
            JetLabel,
            JetButton,
            JetInputError,
        },
        data() {
            return {
                form: this.$inertia.form(
                    {
                        _method: "PUT",
                        title: this.blog.title,
                        content: this.blog.content,
                    },
                    {
                        bag: "blogUpdate",
                        resetOnSuccess: false,
                    }
                )
            };
        },
        methods: {
            editBlog() {
                // console.log(this.blog);
                this.form.post(route("blog.update", this.blog), {
                    errorBag: 'blogUpdate',
                    onError: () => {
                        if (this.form.errors.title) {
                            // console.log('title error');
                            // this.$refs.title.focus()
                        }

                        if (this.form.errors.content) {
                            // console.log('content error');
                            // this.$refs.content.focus()
                        }
                    },
                });
            }
        }
    }
</script>

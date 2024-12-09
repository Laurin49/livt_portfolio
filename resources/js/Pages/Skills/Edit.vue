<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, router, useForm } from '@inertiajs/vue3';

const props = defineProps({
  skill: Object,
});

const form = useForm({
    name: props.skill?.name,
    image: null,
});

const submit = () => {
  router.post(`/skills/${props.skill.id}`, {
    _method: "put",
    name: form.name,
    image: form.image,
  });
};
</script>

<template>
    <Head title="Edit Skill" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">Edit Skill</h2>
        </template>

        <div class="py-12">
            <div class="max-w-md mx-auto bg-white sm:px-6 lg:px-8">
                <form @submit.prevent="submit" class="p-4">
                  <div>
                      <InputLabel for="name" value="Name" />
                      <TextInput
                          id="name"
                          type="text"
                          class="block w-full mt-1"
                          v-model="form.name"
                          autofocus
                      />
                      <InputError class="mt-2" :message="$page.props.errors.name" />
                  </div>
                  <div class="mt-2">
                      <InputLabel for="image" value="Image" />
                      <TextInput
                          id="image"
                          type="file"
                          class="block w-full mt-1"
                          @input="form.image = $event.target.files[0]"
                      />
                      <InputError class="mt-2" :message="$page.props.errors.image" />
                  </div>
      
      
                  <div class="flex items-center justify-end mt-4">
                      <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                          Update
                      </PrimaryButton>
                  </div>
              </form>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
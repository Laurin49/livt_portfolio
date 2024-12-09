<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, useForm } from '@inertiajs/vue3';

defineProps({
  skills: Array
});

const form = useForm({
    name: '',
    image: null,
    project_url: '',
    skill_id: '',
});

const submit = () => {
    form.post(route('projects.store'));
};
</script>

<template>
    <Head title="New Project" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">New Project</h2>
        </template>

        <div class="py-12">
            <div class="max-w-md mx-auto bg-white sm:px-6 lg:px-8">
                <form @submit.prevent="submit" class="p-4">
                  <div>
                    <InputLabel for="skill_id" value="Skill" />
                    <select 
                      v-model="form.skill_id" id="skill_id" name="skill_id"
                      class="block w-full py-2 pl-3 pr-10 mt-1 text-base border-gray-300 rounded-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm">
                      <option v-for="skill in skills" :key="skill.id" :value="skill.id">{{ skill.name }}</option>
                    </select>
                  </div>
                  <div>
                      <InputLabel for="name" value="Name" />
                      <TextInput
                          id="name"
                          type="text"
                          class="block w-full mt-1"
                          v-model="form.name"
                          autofocus
                      />
                      <InputError class="mt-2" :message="form.errors.name" />
                  </div>
                  <div class="mt-2">
                      <InputLabel for="project_url" value="URL" />
                      <TextInput
                          id="project_url"
                          type="text"
                          class="block w-full mt-1"
                          v-model="form.project_url"
                          autofocus
                      />
                      <InputError class="mt-2" :message="form.errors.project_url" />
                  </div>
                  <div class="mt-2">
                      <InputLabel for="image" value="Image" />
                      <TextInput
                          id="image"
                          type="file"
                          class="block w-full mt-1"
                          @input="form.image = $event.target.files[0]"
                      />
                      <InputError class="mt-2" :message="form.errors.image" />
                  </div>
      
      
                  <div class="flex items-center justify-end mt-4">
                      <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                          Store
                      </PrimaryButton>
                  </div>
              </form>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
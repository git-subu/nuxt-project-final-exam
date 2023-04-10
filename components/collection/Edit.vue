<template>
    <div>
      <!--Edit EMployee modal-->
      <TransitionRoot as="template" :show="openEditModal">
        <Dialog as="div" class="relative z-10" @close="openEditModal = false">
          <TransitionChild
            as="template"
            enter="ease-out duration-300"
            enter-from="opacity-0"
            enter-to="opacity-100"
            leave="ease-in duration-200"
            leave-from="opacity-100"
            leave-to="opacity-0"
          >
            <div
              class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
            />
          </TransitionChild>
  
          <div class="fixed inset-0 z-10 overflow-y-auto">
            <div
              class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0"
            >
              <TransitionChild
                as="template"
                enter="ease-out duration-300"
                enter-from="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                enter-to="opacity-100 translate-y-0 sm:scale-100"
                leave="ease-in duration-200"
                leave-from="opacity-100 translate-y-0 sm:scale-100"
                leave-to="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
              >
                <DialogPanel
                  class="relative transform overflow-hidden rounded-lg bg-white px-4 pb-4 pt-5 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg sm:p-6"
                >
                  <div>
                    <label
                      for="email"
                      class="block text-sm font-medium leading-6 text-gray-900"
                      >Edit EMPLOYEE</label
                    >
                    <div class="mt-2">
                      <label
                        for="email"
                        class="block text-sm font-medium leading-6 text-gray-900"
                        >NAME</label
                      >
                      <input
                        placeholder=" Enter name"
                        v-model="props.editEmployeeData.emp_name"
                        type="text"
                        name="email"
                        id="email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
  
                    <div class="mt-2">
                      <label
                        for="email"
                        class="block text-sm font-medium leading-6 text-gray-900"
                        >AGE</label
                      >
                      <input
                        placeholder=" Enter Age"
                        v-model="props.editEmployeeData.emp_age"
                        type="text"
                        name="email"
                        id="email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                    <div class="mt-2">
                      <label
                        for="email"
                        class="block text-sm font-medium leading-6 text-gray-900"
                        >Gender</label
                      >
                      <input
                        placeholder=" Enter Gender"
                        v-model="props.editEmployeeData.gender"
                        type="text"
                        name="email"
                        id="email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                    <div class="mt-2">
                      <label
                        for="email"
                        class="block text-sm font-medium leading-6 text-gray-900"
                        >Date of Joining</label
                      >
                      <input
                        placeholder=" Enter Date of-join"
                        v-model="props.editEmployeeData.date_join"
                        type="text"
                        name="email"
                        id="email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                    <div class="mt-2">
                      <label
                        for="email"
                        class="block text-sm font-medium leading-6 text-gray-900"
                        >Designation</label
                      >
                      <input
                        placeholder=" Enter Designation"
                        v-model="props.editEmployeeData.designation"
                        type="text"
                        name="email"
                        id="email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                      />
                    </div>
                    <div
                      class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
                    >
                      <button
                        type="button"
                        class="inline-flex w-full justify-center rounded-md bg-gray-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                        @click="editEmployee()"
                      >
                        Update
                      </button>
  
                      <button
                        type="button"
                        class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                        @click="openEditModal = false"
                      >
                        Cancel
                      </button>
                    </div>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </template>
  <script setup>
  import {
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    Dialog,
    DialogPanel,
    DialogTitle,
    TransitionChild,
    TransitionRoot,
  } from "@headlessui/vue";
  // Define props
  const props = defineProps({
    openEditModal: Boolean,
    editEmployeeData: {
      type: Object,
      default: () => {},
    },
  });
  
  // Define emit events
  const emit = defineEmits(["editEmployee"]);
  const editEmployee = () => {
    emit("editEmployee", props.editEmployeeData);
    props.editEmployeeData = {};
  };
  </script>
  
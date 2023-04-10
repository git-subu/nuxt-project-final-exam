<template>
    <div>
      <!--Display employee details-->
      <table class="min-w-full divide-y divide-gray-300">
        <thead class="bg-gray-50">
          <tr>
            <th
              scope="col"
              class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
            >
              NAME
            </th>
  
            <th
              scope="col"
              class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
            >
              AGE
            </th>
            <th
              scope="col"
              class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
            >
              Gender
            </th>
            <th
              scope="col"
              class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
            >
              Date Of Joining
            </th>
            <th
              scope="col"
              class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900"
            >
              Designation
            </th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-200 bg-white">
          <tr v-for="(user, index) in employerData" :key="index">
            <td
              class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
            >
              {{ user.emp_name }}
            </td>
            <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
              {{ user.emp_age }}
            </td>
            <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
              {{ user.gender }}
            </td>
            <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
              {{ user.date_join }}
            </td>
            <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
              {{ user.designation }}
            </td>
            <!--Edit Action-->
            <td class="">
              <PencilSquareIcon
                class="h-5 w-5 mr-3"
                @click="emit('employPrefillData', user, index)"
                aria-hidden="true"
              ></PencilSquareIcon>
              <!--Delete Action-->
              <TrashIcon
                class="h-5 w-5"
                aria-hidden="true"
                @click="(open = true), (deleteIndex = index)"
              ></TrashIcon>
            </td>
          </tr>
        </tbody>
      </table>
      <!--Delete modal-->
      <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-10" @close="open = false">
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
                    <div class="mt-3 text-center sm:mt-5">
                      <DialogTitle
                        as="h3"
                        class="text-base font-semibold leading-6 text-black border-spacing-1"
                        >Delete Confirmation</DialogTitle
                      >
                      <p class="h2 mt-3">
                        Are you sure to delete the employee detail. Click on
                        delete to continue
                      </p>
                    </div>
                  </div>
                  <div
                    class="mt-5 sm:mt-6 sm:grid sm:grid-flow-row-dense sm:grid-cols-2 sm:gap-3"
                  >
                    <button
                      type="button"
                      class="inline-flex w-full justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 sm:col-start-2"
                      @click="deleteDetails(deleteIndex)"
                    >
                      Delete
                    </button>
                    <button
                      type="button"
                      class="mt-3 inline-flex w-full justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50 sm:col-start-1 sm:mt-0"
                      @click="open = false"
                      ref="cancelButtonRef"
                    >
                      Cancel
                    </button>
                  </div>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { defineProps, defineEmits } from "vue";
  import {
    XMarkIcon,
    TrashIcon,
    PencilSquareIcon,
    CheckIcon,
  } from "@heroicons/vue/24/outline";
  import {
    Dialog,
    DialogPanel,
    DialogTitle,
    TransitionChild,
    TransitionRoot,
  } from "@headlessui/vue";
  const open = ref(false);
  const deleteIndex = ref(0);
  // Define props
  const propsdata = defineProps({
    employerData: {
      type: Object,
      default: () => {},
    },
  });
  
  // Define emit events
  const emit = defineEmits(["employPrefillData", "deleteDetails"]);
  // Delete employee
  const deleteDetails = (data: any) => {
    emit("deleteDetails", data);
    open.value = false;
  };
  </script>
  
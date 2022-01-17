<template>
    <Listbox v-if="show" v-model="idOfSelected" as="div">
        <ListboxLabel class="block">
            <slot name="label" />
        </ListboxLabel>
        <div class="relative mt-1">
            <ListboxButton class="relative w-full cursor-pointer sm:text-sm">
                <slot name="button" />
            </ListboxButton>
            <transition
                leave-active-class="transition duration-100 ease-in"
                leave-from-class="opacity-100"
                leave-to-class="opacity-0"
            >
                <ListboxOptions
                    class="
                        absolute
                        z-10
                        w-full
                        overflow-auto
                        text-base
                        rounded-md
                        shadow-lg
                        cursor-pointer
                        max-h-60
                        ring-1 ring-black ring-opacity-5
                        focus:outline-none
                        sm:text-sm
                    "
                >
                    <div v-if="!loading">
                        <ListboxOption
                            v-for="option in options"
                            :key="option[subKey]"
                            v-slot="{ active, selected }"
                            :value="option[subKey]"
                            as="template"
                        >
                            <div class="">
                                <slot
                                    :active="active"
                                    :option="option"
                                    :selected="selected"
                                    name="option"
                                />
                            </div>
                        </ListboxOption>
                    </div>
                    <div v-else class="flex items-center justify-center">
                        <slot name="loader" />
                    </div>
                </ListboxOptions>
            </transition>
        </div>
        <slot name="message" />
    </Listbox>
</template>

<script>
import { defineComponent } from "vue";
import {
    Listbox,
    ListboxButton,
    ListboxLabel,
    ListboxOption,
    ListboxOptions,
} from "@headlessui/vue";

export default defineComponent({
    name: "Selector",
    props: {
        options: Array,
        idOfSelected: String,
        show: Boolean,
        label: String,
        subKey: { type: String, default: "id" },
        loading: { type: Boolean, default: false },
    },
    mounted() {
        console.log("selector mounted");
    },
    components: {
        Listbox,
        ListboxButton,
        ListboxLabel,
        ListboxOption,
        ListboxOptions,
    },
    watch: {
        idOfSelected(val, oldVal) {
            this.$emit("select", val);
        },
    },
});
</script>

<style scoped>
</style>

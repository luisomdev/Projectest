<script setup lang="ts">
import { Button } from "@/components/ui/button";
import { Icon } from "@iconify/vue";
import { useColorMode } from '@vueuse/core'
import { useToast } from "@/components/ui/toast/use-toast";
import { Toaster } from "@/components/ui/toast";
import { onBeforeMount, ref, watch } from "vue";

const { toast } = useToast()
const mode = useColorMode({ disableTransition: false })
const themeText = ref(mode.value)

onBeforeMount(() => themeText.value = mode.value === 'light' ? 'dark' : 'light')
watch(mode, (value) => themeText.value = value === 'light' ? 'dark' : 'light')

const changeTheme = () => {
    toast({
        title: 'Change theme to ${mode.value}',
        description: 'theme updated'
    })
}

</script>


<template>

    <nav class="w-full h-20 flex px-6 md:justify-between items-center">

        <div class="flex justify-center items-center">
            <Icon icon="mdi:bird" width="48" height="48" />
            <span class="text-xl font-bold px-4"> VeterinCap </span>

        </div>

        <div class="flex">

            <Button @click="() => {
                mode = mode == 'light' ? 'dark' : 'light'
                toast({
                    title: `Theme change to ${mode}`,
                    description: 'Updated configuration of theme'
                })
            }">

                <Icon class="transition-all duration-500 "
                    :class="mode == 'light' ? 'opacity-100 scale-100 rotate-0' : 'opacity-100 scale-100 rotate-180'"
                    icon="mdi:sun-moon-stars" />

                Theme to {{ themeText }}
            </Button>

        </div>

    </nav>

    <Toaster />

</template>

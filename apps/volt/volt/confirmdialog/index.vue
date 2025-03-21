<template>
    <ConfirmDialog
        unstyled
        :pt="theme"
        :ptOptions="{
            mergeProps: ptViewMerge
        }"
    >
        <template #container="{ message, acceptCallback, rejectCallback }">
            <div class="flex items-center justify-between shrink-0 p-5">
                <span class="font-semibold text-xl">{{ message.header }}</span>
                <SecondaryButton variant="text" rounded @click="rejectCallback" autofocus>
                    <template #icon>
                        <TimesIcon />
                    </template>
                </SecondaryButton>
            </div>
            <div class="overflow-y-auto pt-0 px-5 pb-5 flex items-center gap-4">
                <ExclamationTriange class="size-6" />
                {{ message.message }}
            </div>
            <div class="pt-0 px-5 pb-5 flex justify-end gap-2">
                <SecondaryButton @click="rejectCallback" :label="message.rejectProps.label" size="small" />
                <Button @click="acceptCallback" :label="message.acceptProps.label" size="small" />
            </div>
        </template>
    </ConfirmDialog>
</template>

<script setup>
import ExclamationTriange from '@primevue/icons/exclamationtriangle';
import TimesIcon from '@primevue/icons/times';
import ConfirmDialog from 'primevue/confirmdialog';
import { ref } from 'vue';
import Button from '../button';
import SecondaryButton from '../button/secondary';
import { ptViewMerge } from '../utils';

const theme = ref({
    root: `max-h-[90%] max-w-screen rounded-xl
        border border-surface-200 dark:border-surface-700
        bg-surface-0 dark:bg-surface-900
        text-surface-700 dark:text-surface-0 shadow-lg`,
    mask: `bg-black/50 fixed top-0 start-0 w-full h-full`,
    transition: {
        enterFromClass: 'opacity-0 scale-75',
        enterActiveClass: 'transition-all duration-150 ease-[cubic-bezier(0,0,0.2,1)]',
        leaveActiveClass: 'transition-all duration-150 ease-[cubic-bezier(0.4,0,0.2,1)]',
        leaveToClass: 'opacity-0 scale-75'
    }
});
</script>

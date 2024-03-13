<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';

defineProps({
    phpVersion: {
        type: String,
        required: true,
    },
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};

function handleImageError() {
    document.getElementById('screenshot-container')?.classList.add('!hidden');
    document.getElementById('docs-card')?.classList.add('!row-span-1');
    document.getElementById('docs-card-content')?.classList.add('!flex-row');
    document.getElementById('background')?.classList.add('!hidden');
}
</script>

<template>

    <Head title="Home" />
    <div class="bg-gray-50 text-black/50 dark:bg-black dark:text-white/50">
        <svg id="background" class="absolute -left-20 top-0 max-w-[877px]" xmlns="http://www.w3.org/2000/svg"
            fill="none" viewBox="0 0 877 968">
            <g clip-path="url(#a)">
                <circle cx="391" cy="391" r="390.5" stroke="#8a8ee2" transform="matrix(-1 0 0 1 416 -56)" />
                <circle cx="468" cy="468" r="467.5" stroke="#8a8ee2" opacity=".3"
                    transform="matrix(-1 0 0 1 493 -133)" />
                <circle cx="558" cy="558" r="557.5" stroke="#8a8ee2" opacity=".1"
                    transform="matrix(-1 0 0 1 583 -223)" />
                <g filter="url(#b)">
                    <ellipse cx="583" cy="229.5" fill="#8a8ee2" rx="583" ry="229.5"
                        transform="matrix(-1 0 0 1 621 -9)" />
                </g>
                <g filter="url(#c)">
                    <ellipse cx="262" cy="184.5" fill="#fff" rx="262" ry="184.5" transform="matrix(-1 0 0 1 99 42)" />
                </g>
            </g>
            <defs>
                <filter id="b" width="1614" height="907" x="-769" y="-233" color-interpolation-filters="sRGB"
                    filterUnits="userSpaceOnUse">
                    <feFlood flood-opacity="0" result="BackgroundImageFix" />
                    <feBlend in="SourceGraphic" in2="BackgroundImageFix" result="shape" />
                    <feGaussianBlur result="effect1_foregroundBlur_3089_39042" stdDeviation="112" />
                </filter>
                <filter id="c" width="972" height="817" x="-649" y="-182" color-interpolation-filters="sRGB"
                    filterUnits="userSpaceOnUse">
                    <feFlood flood-opacity="0" result="BackgroundImageFix" />
                    <feBlend in="SourceGraphic" in2="BackgroundImageFix" result="shape" />
                    <feGaussianBlur result="effect1_foregroundBlur_3089_39042" stdDeviation="112" />
                </filter>
                <clipPath id="a">
                    <path fill="#fff" d="M877 0H0v968h877z" />
                </clipPath>
            </defs>
        </svg>

        <div
            class="relative min-h-screen flex flex-col items-center justify-center selection:bg-[#8a8ee2] selection:text-white">
            <div class="relative w-full max-w-2xl px-6 lg:max-w-7xl">
                <header class="grid grid-cols-2 items-center gap-2 py-10 lg:grid-cols-3">
                    <div class="flex lg:justify-center lg:col-start-2">
                        <img src="/img/logo.svg" class="h-12 w-auto lg:h-16" alt="">
                    </div>
                </header>

                <main class="mt-6">
                    <div class="grid gap-6 lg:grid-cols-2 lg:gap-8">
                        <div
                            class="flex flex-col items-start gap-6 overflow-hidden rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] md:row-span-3 lg:p-10 lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20]">

                            <div class="relative flex items-center gap-6 lg:items-end">
                                <div id="docs-card-content" class="flex items-start gap-6 lg:flex-col">
                                    <div class="pt-3 sm:pt-5 lg:pt-0">
                                        <h2 class="text-xl font-semibold text-black dark:text-white">Winkel planogram
                                        </h2>

                                        <p class="mt-4 text-sm/relaxed">
                                            Speciaal voor Amac Nijmegen is er nu een planogram app voor de kasten in de
                                            winkel. Hiermee kan je makkelijk de kasten inrichten en aanpassen. Ook kan
                                            je de producten in de kasten aanpassen en toevoegen (met een admin account).
                                        </p>

                                        <div class="mt-12">
                                            <form @submit.prevent="submit">
                                                <div>
                                                    <InputLabel for="email" value="Gebruikersnaam" />

                                                    <TextInput id="email" type="email" class="mt-1 block w-full"
                                                        v-model="form.email" required autofocus
                                                        autocomplete="username" />

                                                    <InputError class="mt-2" :message="form.errors.email" />
                                                </div>

                                                <div class="mt-4">
                                                    <InputLabel for="password" value="Wachtwoord" />

                                                    <TextInput id="password" type="password" class="mt-1 block w-full"
                                                        v-model="form.password" required
                                                        autocomplete="current-password" />

                                                    <InputError class="mt-2" :message="form.errors.password" />
                                                </div>

                                                <div class="block mt-4">
                                                    <label class="flex items-center">
                                                        <Checkbox name="remember" v-model:checked="form.remember" />
                                                        <span
                                                            class="ms-2 text-sm text-gray-600 dark:text-gray-400">Onthoud mij</span>
                                                    </label>
                                                </div>

                                                <div class="flex items-center justify-end mt-4">
                                                    <Link v-if="canResetPassword" :href="route('password.request')"
                                                        class="underline text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-gray-100 rounded-md focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 dark:focus:ring-offset-gray-800">
                                                    Wachtwoord vergeten?
                                                    </Link>

                                                    <PrimaryButton class="ms-4"
                                                        :class="{ 'opacity-25': form.processing }"
                                                        :disabled="form.processing">
                                                        Log in
                                                    </PrimaryButton>
                                                </div>
                                            </form>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <a href="https://amac.nl"
                            class="flex items-start gap-4 rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20]">
                            <div
                                class="flex size-12 shrink-0 items-center justify-center rounded-full bg-[#8a8ee2]/10 sm:size-16">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                    stroke-width="1.5" stroke="#8a8ee2" class="size-6 sm:size-7">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                        d="M15.75 10.5V6a3.75 3.75 0 1 0-7.5 0v4.5m11.356-1.993 1.263 12c.07.665-.45 1.243-1.119 1.243H4.25a1.125 1.125 0 0 1-1.12-1.243l1.264-12A1.125 1.125 0 0 1 5.513 7.5h12.974c.576 0 1.059.435 1.119 1.007ZM8.625 10.5a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm7.5 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Z" />
                                </svg>
                            </div>

                            <div class="pt-3 sm:pt-5">
                                <h2 class="text-xl font-semibold text-black dark:text-white">Amac Webshop <span
                                        class="text-sm text-gray-500">(Externe link)</span></h2>

                                <p class="mt-4 text-sm/relaxed">
                                    Bekijk de webshop van Amac. Hier kan je alle producten die Amac verkoopt vinden en
                                    bestellen. Ook kan je hier snel de voorraad van een artikel in de winkel bekijken.
                                </p>
                            </div>

                            <svg class="size-6 shrink-0 self-center stroke-[#8a8ee2]" xmlns="http://www.w3.org/2000/svg"
                                fill="none" viewBox="0 0 24 24" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75" />
                            </svg>
                        </a>

                        <a href="https://personeel.amac.nl"
                            class="flex items-start gap-4 rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] transition duration-300 hover:text-black/70 hover:ring-black/20 focus:outline-none focus-visible:ring-[#FF2D20] lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800 dark:hover:text-white/70 dark:hover:ring-zinc-700 dark:focus-visible:ring-[#FF2D20]">
                            <div
                                class="flex size-12 shrink-0 items-center justify-center rounded-full bg-[#8a8ee2]/10 sm:size-16">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                    stroke-width="1.5" stroke="#8a8ee2" class="size-6 sm:size-7">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                        d="M2.25 7.125C2.25 6.504 2.754 6 3.375 6h6c.621 0 1.125.504 1.125 1.125v3.75c0 .621-.504 1.125-1.125 1.125h-6a1.125 1.125 0 0 1-1.125-1.125v-3.75ZM14.25 8.625c0-.621.504-1.125 1.125-1.125h5.25c.621 0 1.125.504 1.125 1.125v8.25c0 .621-.504 1.125-1.125 1.125h-5.25a1.125 1.125 0 0 1-1.125-1.125v-8.25ZM3.75 16.125c0-.621.504-1.125 1.125-1.125h5.25c.621 0 1.125.504 1.125 1.125v2.25c0 .621-.504 1.125-1.125 1.125h-5.25a1.125 1.125 0 0 1-1.125-1.125v-2.25Z" />
                                </svg>
                            </div>

                            <div class="pt-3 sm:pt-5">
                                <h2 class="text-xl font-semibold text-black dark:text-white">Amac Planner <span
                                        class="text-sm text-gray-500">(Externe link)</span></h2>

                                <p class="mt-4 text-sm/relaxed">
                                    Bekijk je persoonlijke planning en teamplanning. Ook kan je hier de Amac Academy
                                    trainingen volgen, hiermee kan je jezelf verder ontwikkelen en je kennis verbreden.
                                </p>
                            </div>

                            <svg class="size-6 shrink-0 self-center stroke-[#8a8ee2]" xmlns="http://www.w3.org/2000/svg"
                                fill="none" viewBox="0 0 24 24" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75" />
                            </svg>
                        </a>

                        <div
                            class="flex items-start gap-4 rounded-lg bg-white p-6 shadow-[0px_14px_34px_0px_rgba(0,0,0,0.08)] ring-1 ring-white/[0.05] lg:pb-10 dark:bg-zinc-900 dark:ring-zinc-800">
                            <div
                                class="flex size-12 shrink-0 items-center justify-center rounded-full bg-[#8a8ee2]/10 sm:size-16">
                                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                    stroke-width="1.5" stroke="#8a8ee2" class="size-6 sm:size-7">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                        d="M20.25 14.15v4.25c0 1.094-.787 2.036-1.872 2.18-2.087.277-4.216.42-6.378.42s-4.291-.143-6.378-.42c-1.085-.144-1.872-1.086-1.872-2.18v-4.25m16.5 0a2.18 2.18 0 0 0 .75-1.661V8.706c0-1.081-.768-2.015-1.837-2.175a48.114 48.114 0 0 0-3.413-.387m4.5 8.006c-.194.165-.42.295-.673.38A23.978 23.978 0 0 1 12 15.75c-2.648 0-5.195-.429-7.577-1.22a2.016 2.016 0 0 1-.673-.38m0 0A2.18 2.18 0 0 1 3 12.489V8.706c0-1.081.768-2.015 1.837-2.175a48.111 48.111 0 0 1 3.413-.387m7.5 0V5.25A2.25 2.25 0 0 0 13.5 3h-3a2.25 2.25 0 0 0-2.25 2.25v.894m7.5 0a48.667 48.667 0 0 0-7.5 0M12 12.75h.008v.008H12v-.008Z" />
                                </svg>
                            </div>

                            <div class="pt-3 sm:pt-5">
                                <h2 class="text-xl font-semibold text-black dark:text-white">Amac HR2day <span
                                        class="text-sm text-gray-500">(Externe link)</span></h2>

                                <p class="mt-4 text-sm/relaxed">
                                    Bekijk je persoonlijke gegevens, zoals je loonstrook en vakantiedagen. Ook kan je
                                    hier je persoonlijke gegevens aanpassen.
                                </p>
                            </div>

                            <svg class="size-6 shrink-0 self-center stroke-[#8a8ee2]" xmlns="http://www.w3.org/2000/svg"
                                fill="none" viewBox="0 0 24 24" stroke-width="1.5">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                    d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75" />
                            </svg>
                        </div>
                    </div>
                </main>

                <footer class="py-16 text-center text-sm text-black dark:text-white/70">
                    aPRplano v0.0.1 (PHP v{{ phpVersion }}) - Alleen voor intern gebruik.
                </footer>
            </div>
        </div>
    </div>
</template>

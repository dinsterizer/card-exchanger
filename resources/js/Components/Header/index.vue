<script setup>
import {
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    Popover,
    PopoverButton,
    PopoverOverlay,
    PopoverPanel,
    TransitionChild,
    TransitionRoot,
} from '@headlessui/vue';
import { BellIcon, MenuIcon, XIcon } from '@heroicons/vue/outline';
import { SearchIcon } from '@heroicons/vue/solid';
import { Link } from '@inertiajs/inertia-vue3';

const user = {
    name: 'Chelsea Hagon',
    email: 'chelseahagon@example.com',
    role: 'Human Resources Manager',
    imageUrl:
        'https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
};
const navigation = [
    { name: 'Trang chủ', href: '/', current: true },
    { name: 'Đổi thẻ cào', href: '/cards/exchange', current: false },
    { name: 'Lịch sử', href: '/cards/history', current: false },
];
const userNavigation = [
    { name: 'Hồ sơ', href: '#' },
    { name: 'Cài đặt', href: '#' },
    { name: 'Đăng xuất', href: '#' },
];
</script>

<template>
    <Popover as="header" v-slot="{ open }">
        <div
            class="
                relative
                flex flex-wrap
                items-center
                justify-center
                lg:justify-between
            "
        >
            <!-- Logo -->
            <div class="absolute left-0 py-5 flex-shrink-0 lg:static">
                <Link href="#">
                    <span class="sr-only">Workflow</span>
                    <!-- https://tailwindui.com/img/logos/workflow-mark-cyan-200.svg -->
                    <svg
                        class="h-8 w-auto"
                        fill="none"
                        viewBox="0 0 35 32"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            fill="#A5F3FC"
                            d="M15.258 26.865a4.043 4.043 0 01-1.133 2.917A4.006 4.006 0 0111.253 31a3.992 3.992 0 01-2.872-1.218 4.028 4.028 0 01-1.133-2.917c.009-.698.2-1.382.557-1.981.356-.6.863-1.094 1.47-1.433-.024.109.09-.055 0 0l1.86-1.652a8.495 8.495 0 002.304-5.793c0-2.926-1.711-5.901-4.17-7.457.094.055-.036-.094 0 0A3.952 3.952 0 017.8 7.116a3.975 3.975 0 01-.557-1.98 4.042 4.042 0 011.133-2.918A4.006 4.006 0 0111.247 1a3.99 3.99 0 012.872 1.218 4.025 4.025 0 011.133 2.917 8.521 8.521 0 002.347 5.832l.817.8c.326.285.668.551 1.024.798.621.33 1.142.826 1.504 1.431a3.902 3.902 0 01-1.504 5.442c.033-.067-.063.036 0 0a8.968 8.968 0 00-3.024 3.183 9.016 9.016 0 00-1.158 4.244zM19.741 5.123c0 .796.235 1.575.676 2.237a4.01 4.01 0 001.798 1.482 3.99 3.99 0 004.366-.873 4.042 4.042 0 00.869-4.386 4.02 4.02 0 00-1.476-1.806 3.994 3.994 0 00-5.058.501 4.038 4.038 0 00-1.175 2.845zM23.748 22.84c-.792 0-1.567.236-2.226.678a4.021 4.021 0 00-1.476 1.806 4.042 4.042 0 00.869 4.387 3.99 3.99 0 004.366.873A4.01 4.01 0 0027.08 29.1a4.039 4.039 0 00-.5-5.082 4 4 0 00-2.832-1.18zM34 15.994c0-.796-.235-1.574-.675-2.236a4.01 4.01 0 00-1.798-1.483 3.99 3.99 0 00-4.367.873 4.042 4.042 0 00-.869 4.387 4.02 4.02 0 001.476 1.806 3.993 3.993 0 002.226.678 4.003 4.003 0 002.832-1.18A4.04 4.04 0 0034 15.993z M5.007 11.969c-.793 0-1.567.236-2.226.678a4.021 4.021 0 00-1.476 1.807 4.042 4.042 0 00.869 4.386 4.001 4.001 0 004.366.873 4.011 4.011 0 001.798-1.483 4.038 4.038 0 00-.5-5.08 4.004 4.004 0 00-2.831-1.181z"
                        />
                    </svg>
                </Link>
            </div>

            <!-- Right section on desktop -->
            <div
                class="hidden lg:ml-4 lg:flex lg:items-center lg:py-5 lg:pr-0.5"
            >
                <button
                    type="button"
                    class="
                        flex-shrink-0
                        p-1
                        text-cyan-200
                        rounded-full
                        hover:text-white hover:bg-white hover:bg-opacity-10
                        focus:outline-none focus:ring-2 focus:ring-white
                    "
                >
                    <span class="sr-only">View notifications</span>
                    <BellIcon class="h-6 w-6" aria-hidden="true" />
                </button>

                <!-- Profile dropdown -->
                <!-- <Menu as="div" class="ml-4 relative flex-shrink-0">
                    <div>
                        <MenuButton
                            class="
                                bg-white
                                rounded-full
                                flex
                                text-sm
                                ring-2 ring-white ring-opacity-20
                                focus:outline-none focus:ring-opacity-100
                            "
                        >
                            <span class="sr-only">Open user menu</span>
                            <img
                                class="h-8 w-8 rounded-full"
                                :src="user.imageUrl"
                                alt=""
                            />
                        </MenuButton>
                    </div>
                    <transition
                        leave-active-class="transition ease-in duration-75"
                        leave-from-class="transform opacity-100 scale-100"
                        leave-to-class="transform opacity-0 scale-95"
                    >
                        <MenuItems
                            class="
                                origin-top-right
                                z-40
                                absolute
                                -right-2
                                mt-2
                                w-48
                                rounded-md
                                shadow-lg
                                py-1
                                bg-white
                                ring-1 ring-black ring-opacity-5
                                focus:outline-none
                            "
                        >
                            <MenuItem
                                v-for="item in userNavigation"
                                :key="item.name"
                                v-slot="{ active }"
                            >
                                <Link
                                    :href="item.href"
                                    :class="[
                                        active ? 'bg-gray-100' : '',
                                        'block px-4 py-2 text-sm text-gray-700',
                                    ]"
                                    >{{ item.name }}</
                                >
                            </MenuItem>
                        </MenuItems>
                    </transition>
                </Menu> -->
            </div>

            <div
                class="
                    w-full
                    py-5
                    lg:border-t lg:border-white lg:border-opacity-20
                "
            >
                <div class="lg:grid lg:grid-cols-3 lg:gap-8 lg:items-center">
                    <!-- Left nav -->
                    <div class="hidden lg:block lg:col-span-2">
                        <nav class="flex space-x-4">
                            <Link
                                v-for="item in navigation"
                                :key="item.name"
                                :href="item.href"
                                :class="[
                                    item.current
                                        ? 'text-white'
                                        : 'text-cyan-100',
                                    'text-sm font-medium rounded-md bg-white bg-opacity-0 px-3 py-2 hover:bg-opacity-10',
                                ]"
                                :aria-current="
                                    item.current ? 'page' : undefined
                                "
                            >
                                {{ item.name }}
                            </Link>
                        </nav>
                    </div>
                    <div class="px-12 lg:px-0">
                        <!-- Search -->
                        <div class="max-w-xs mx-auto w-full lg:max-w-md">
                            <label for="search" class="sr-only">Search</label>
                            <div
                                class="
                                    relative
                                    text-white
                                    focus-within:text-gray-600
                                "
                            >
                                <div
                                    class="
                                        pointer-events-none
                                        absolute
                                        inset-y-0
                                        left-0
                                        pl-3
                                        flex
                                        items-center
                                    "
                                >
                                    <SearchIcon
                                        class="h-5 w-5"
                                        aria-hidden="true"
                                    />
                                </div>
                                <input
                                    id="search"
                                    class="
                                        block
                                        w-full
                                        text-white
                                        bg-white bg-opacity-20
                                        py-2
                                        pl-10
                                        pr-3
                                        border border-transparent
                                        rounded-md
                                        leading-5
                                        focus:text-gray-900
                                        placeholder-white
                                        focus:outline-none
                                        focus:bg-opacity-100
                                        focus:border-transparent
                                        focus:placeholder-gray-500
                                        focus:ring-0
                                        sm:text-sm
                                    "
                                    placeholder="Search"
                                    type="search"
                                    name="search"
                                />
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Menu button -->
            <div class="absolute right-0 flex-shrink-0 lg:hidden">
                <!-- Mobile menu button -->
                <PopoverButton
                    class="
                        bg-transparent
                        p-2
                        rounded-md
                        inline-flex
                        items-center
                        justify-center
                        text-cyan-200
                        hover:text-white hover:bg-white hover:bg-opacity-10
                        focus:outline-none focus:ring-2 focus:ring-white
                    "
                >
                    <span class="sr-only">Open main menu</span>
                    <MenuIcon
                        v-if="!open"
                        class="block h-6 w-6"
                        aria-hidden="true"
                    />
                    <XIcon v-else class="block h-6 w-6" aria-hidden="true" />
                </PopoverButton>
            </div>
        </div>

        <TransitionRoot as="template" :show="open">
            <div class="lg:hidden">
                <TransitionChild
                    as="template"
                    enter="duration-150 ease-out"
                    enter-from="opacity-0"
                    enter-to="opacity-100"
                    leave="duration-150 ease-in"
                    leave-from="opacity-100"
                    leave-to="opacity-0"
                >
                    <PopoverOverlay
                        class="z-20 fixed inset-0 bg-black bg-opacity-25"
                    />
                </TransitionChild>

                <TransitionChild
                    as="template"
                    enter="duration-150 ease-out"
                    enter-from="opacity-0 scale-95"
                    enter-to="opacity-100 scale-100"
                    leave="duration-150 ease-in"
                    leave-from="opacity-100 scale-100"
                    leave-to="opacity-0 scale-95"
                >
                    <PopoverPanel
                        focus
                        class="
                            z-30
                            absolute
                            top-0
                            inset-x-0
                            max-w-3xl
                            mx-auto
                            w-full
                            p-2
                            transition
                            transform
                            origin-top
                        "
                    >
                        <div
                            class="
                                rounded-lg
                                shadow-lg
                                ring-1 ring-black ring-opacity-5
                                bg-white
                                divide-y divide-gray-200
                            "
                        >
                            <div class="pt-3 pb-2">
                                <div
                                    class="
                                        flex
                                        items-center
                                        justify-between
                                        px-4
                                    "
                                >
                                    <div>
                                        <img
                                            class="h-8 w-auto"
                                            src="https://tailwindui.com/img/logos/workflow-mark-cyan-600.svg"
                                            alt="Workflow"
                                        />
                                    </div>
                                    <div class="-mr-2">
                                        <PopoverButton
                                            class="
                                                bg-white
                                                rounded-md
                                                p-2
                                                inline-flex
                                                items-center
                                                justify-center
                                                text-gray-400
                                                hover:text-gray-500
                                                hover:bg-gray-100
                                                focus:outline-none
                                                focus:ring-2
                                                focus:ring-inset
                                                focus:ring-cyan-500
                                            "
                                        >
                                            <span class="sr-only">
                                                Close menu
                                            </span>
                                            <XIcon
                                                class="h-6 w-6"
                                                aria-hidden="true"
                                            />
                                        </PopoverButton>
                                    </div>
                                </div>
                                <div class="mt-3 px-2 space-y-1">
                                    <Link
                                        v-for="item in navigation"
                                        :key="item.name"
                                        :href="item.href"
                                        class="
                                            block
                                            rounded-md
                                            px-3
                                            py-2
                                            text-base text-gray-900
                                            font-medium
                                            hover:bg-gray-100
                                            hover:text-gray-800
                                        "
                                        >{{ item.name }}</Link
                                    >
                                </div>
                            </div>
                            <!-- <div class="pt-4 pb-2">
                                <div class="flex items-center px-5">
                                    <div class="flex-shrink-0">
                                        <img
                                            class="h-10 w-10 rounded-full"
                                            :src="user.imageUrl"
                                            alt=""
                                        />
                                    </div>
                                    <div class="ml-3 min-w-0 flex-1">
                                        <div
                                            class="
                                                text-base
                                                font-medium
                                                text-gray-800
                                                truncate
                                            "
                                        >
                                            {{ user.name }}
                                        </div>
                                        <div
                                            class="
                                                text-sm
                                                font-medium
                                                text-gray-500
                                                truncate
                                            "
                                        >
                                            {{ user.email }}
                                        </div>
                                    </div>
                                    <button
                                        type="button"
                                        class="
                                            ml-auto
                                            flex-shrink-0
                                            bg-white
                                            p-1
                                            text-gray-400
                                            rounded-full
                                            hover:text-gray-500
                                            focus:outline-none
                                            focus:ring-2
                                            focus:ring-offset-2
                                            focus:ring-cyan-500
                                        "
                                    >
                                        <span class="sr-only"
                                            >View notifications</span
                                        >
                                        <BellIcon
                                            class="h-6 w-6"
                                            aria-hidden="true"
                                        />
                                    </button>
                                </div>
                                <div class="mt-3 px-2 space-y-1">
                                    <Link
                                        v-for="item in userNavigation"
                                        :key="item.name"
                                        :href="item.href"
                                        class="
                                            block
                                            rounded-md
                                            px-3
                                            py-2
                                            text-base text-gray-900
                                            font-medium
                                            hover:bg-gray-100
                                            hover:text-gray-800
                                        "
                                        >{{ item.name }}</
                                    >
                                </div>
                            </div> -->
                        </div>
                    </PopoverPanel>
                </TransitionChild>
            </div>
        </TransitionRoot>
    </Popover>
</template>

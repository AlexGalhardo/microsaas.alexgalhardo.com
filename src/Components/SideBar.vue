<template>
    <aside
        id="logo-sidebar"
        class="fixed top-0 left-0 z-40 w-64 h-screen pt-20 transition-transform -translate-x-full bg-white border-r sm:translate-x-0"
        aria-label="Sidebar"
    >
        <div class="h-full px-3 pb-4 overflow-y-auto bg-white">
            <ul class="space-y-2 font-medium">
                <li>
                    <a
                        href="/"
                        class="flex items-center p-2 rounded-lg hover:bg-gray-200 group"
                    >
                        <i class="bi bi-clipboard-data"></i>
                        <span class="flex-1 ms-3 whitespace-nowrap">Home</span>
                    </a>
                </li>
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-mailbox"></i>
                        <span class="flex-1 ms-3 whitespace-nowrap">Transactions</span>
                        <span
                            class="inline-flex items-center justify-center w-3 h-3 p-3 ms-3 text-sm font-medium text-blue-800 bg-blue-100 rounded-full"
                            >192</span
                        >
                    </a>
                </li>
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 rounded-lg hover:bg-gray-200 group"
                    >
                        <i class="bi bi-person-fill-gear"></i>
                        <span class="flex-1 ms-3 whitespace-nowrap">Customers</span>
                    </a>
                </li>
            </ul>
            <ul class="pt-4 mt-4 space-y-2 font-medium border-t border-gray-200">
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 transition duration-75 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-fire"></i>
                        <span class="ms-3">Upgrade to Pro</span>
                    </a>
                </li>
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 transition duration-75 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-code"></i>
                        <span class="ms-3">API Documentation</span>
                    </a>
                </li>
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 transition duration-75 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-cone-striped"></i>
                        <span class="ms-3">FAQ</span>
                    </a>
                </li>
                <li>
                    <a
                        href="#"
                        class="flex items-center p-2 transition duration-75 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-envelope"></i>
                        <span class="ms-3">Support</span>
                    </a>
                </li>
                <li>
                    <a
                        href="https://github.com/AlexGalhardo/microsaas.alexgalhardo.com"
                        target="_blank"
                        class="flex items-center p-2 transition duration-75 rounded-lg hover:bg-gray-100 group"
                    >
                        <i class="bi bi-github"></i>
                        <span class="ms-3">Source Code</span>
                    </a>
                </li>
            </ul>
        </div>
    </aside>
</template>

<script>
export default {};
</script>

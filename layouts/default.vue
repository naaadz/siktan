<template>
    <div>
        <Html>
            <Head>
                <Title>SikTan</Title>
            </Head>
            <Body>
                <div class="wrap">
                    <header class="flex bg-black w-full items-center justify-center py-6 gap-2">
                        <i class="mat-ico text-white text-4xl">lyrics</i>
                        <span class="text-4xl text-white">SikTan</span>
                    </header>
                    <div>
                        <slot />
                    </div>
                    <div class="mobile-menu w-3/4 lg:hidden p-10">
                        <ul class="space-y-3">
                            <li><nuxt-link>Solutions</nuxt-link></li>
                            <li><nuxt-link>Platform</nuxt-link></li>
                            <li><nuxt-link>Data</nuxt-link></li>
                            <li><nuxt-link>Customers</nuxt-link></li>
                            <li><nuxt-link>InSites™</nuxt-link></li>
                            <div class="w-full border-b"></div>
                            <li><nuxt-link>Sign in</nuxt-link></li>
                            <li><nuxt-link>Request a demo</nuxt-link></li>
                        </ul>
                    </div>
                </div>
            </Body>
        </Html>	
    </div>
</template>

<script setup>

const route = useRoute()

const data = reactive({
    mobileMenuOpen: false,
    notifyOpen: false
})

const onMobileMenuClick = (payload) => {
    data.mobileMenuOpen = payload
    //console.log('onMobileMenuClick', payload)
}

</script>

<style>
    .toggle-notify {
        position: relative;
        z-index: 100;
    }
</style>
<template>
    <div>
        <NavBar />
        <SideBar />
        <FileUploadSection />
        <div class="p-5 sm:ml-64 mt-5">
            <HomeCharts />
            <FooterSection />
        </div>
    </div>
</template>

<script>
import NavBar from "../Components/NavBar.vue";
import SideBar from "../Components/SideBar.vue";
import HomeCharts from "../Components/HomeCharts.vue";
import FooterSection from "../Components/FooterSection.vue";

export default {
    components: {
        NavBar,
        SideBar,
        HomeCharts,
        FooterSection,
    },
};
</script>

<!--
 * @Description: 主页面
 * @Author: Wangyl
 * @Date: 2021-10-05 17:59:35
 * @LastEditors: Wangyl
 * @LastEditTime: 2022-05-02 15:06:40
-->

<template>
    <div class="about">
        <v-header />
        <v-sidebar />
        <div class="content-box" :class="{ 'content-collapse': collapse }">
            <v-tags></v-tags>
            <br>
            <div class="content">
                <router-view v-slot="{ Component }">
                    <transition name="move" mode="out-in">
                        <keep-alive :include="tagsList">
                            <component :is="Component" />
                        </keep-alive>
                    </transition>
                </router-view>
            </div>
        </div>
    </div>
</template>
<script>
import { computed } from "vue";
import { useStore } from "vuex";
import vHeader from "../components/Header.vue";
import vSidebar from "../components/Sidebar.vue";
import vTags from "../components/Tags.vue";
export default {
    name: "Home",
    components: {
        vHeader,
        vSidebar,
        vTags,
    },
    setup() {
        const store = useStore();
        const tagsList = computed(() =>
            store.state.tagsList.map((item) => item.name)
        );
        const collapse = computed(() => store.state.collapse);
        return {
            tagsList,
            collapse,
        };
    },
};
</script>

<template>
    <div class="sidebar">
        <el-menu
            class="sidebar-el-menu"
            :default-active="onRoutes"
            :collapse="collapse"
            background-color="#324157"
            text-color="#bfcbd9"
            active-text-color="#20a0ff"
            unique-opened
            router
        >
            <template v-for="item in items">
                <template v-if="item.subs">
                    <el-submenu :index="item.index" :key="item.index">
                        <template slot="title">
                            <i :class="item.icon"></i>
                            <span slot="title">{{ item.title }}</span>
                        </template>
                        <template v-for="subItem in item.subs">
                            <el-submenu
                                v-if="subItem.subs"
                                :index="subItem.index"
                                :key="subItem.index"
                            >
                                <template slot="title">{{ subItem.title }}</template>
                                <el-menu-item
                                    v-for="(threeItem,i) in subItem.subs"
                                    :key="i"
                                    :index="threeItem.index"
                                >{{ threeItem.title }}</el-menu-item>
                            </el-submenu>
                            <el-menu-item
                                v-else
                                :index="subItem.index"
                                :key="subItem.index"
                            >{{ subItem.title }}</el-menu-item>
                        </template>
                    </el-submenu>
                </template>
                <template v-else>
                    <el-menu-item :index="item.index" :key="item.index">
                        <i :class="item.icon"></i>
                        <span slot="title">{{ item.title }}</span>
                    </el-menu-item>
                </template>
            </template>
        </el-menu>
    </div>
</template>

<script>
import bus from '../common/bus';
export default {
    data() {
        return {
            collapse: false,
            items: [
                {
                    icon: 'el-icon-lx-home',
                    index: 'dashboard',
                    title: '????????????'
                },
                {
                    icon: 'el-icon-lx-people',
                    index: '1',
                    title: '????????????',
                    subs: [
                        {
                            index: 'users',
                            title: '????????????'
                        },
                        {
                            index: 'address',
                            title: '????????????',
                        },
                        {
                            index: 'advice',
                            title: '????????????'
                        }
                    ]
                },
                {
                    icon: 'el-icon-lx-goods',
                    index: '2',
                    title: '????????????',
                    subs: [
                        {
                            index: 'goodUpd',
                            title: '???????????????',
                        },

                        {
                            index: 'goodCato',
                            title: '????????????',
                        },
                        {
                            index: 'goodpic',
                            title: '????????????',
                        }
                    ]
                },

                {
                    icon: 'el-icon-lx-goods',
                    index: '3',
                    title: '????????????',
                    subs: [
                        {
                            index: 'suggest',
                            title: '???????????????',
                        },
                        {
                            index: 'suggestbig',
                            title: '???????????????',
                        }
                    ]
                },
                {
                    icon: 'el-icon-lx-cascades',
                    index: 'table',
                    title: '????????????',
                },

                {
                    icon: 'el-icon-lx-copy',
                    index: 'tabs',
                    title: 'tab?????????'
                },
                {
                    icon: 'el-icon-lx-calendar',
                    index: '5',
                    title: '????????????',
                    subs: [
                        {
                            index: 'form',
                            title: '????????????'
                        },
                        {
                            index: '3-2',
                            title: '????????????',
                            subs: [
                                {
                                    index: 'editor',
                                    title: '??????????????????'
                                },
                                {
                                    index: 'markdown',
                                    title: 'markdown?????????'
                                }
                            ]
                        },
                        {
                            index: 'upload',
                            title: '????????????'
                        }
                    ]
                },
                {
                    icon: 'el-icon-lx-emoji',
                    index: 'icon',
                    title: '???????????????'
                },
                {
                    icon: 'el-icon-pie-chart',
                    index: 'charts',
                    title: 'schart??????'
                },
                {
                    icon: 'el-icon-rank',
                    index: '6',
                    title: '????????????',
                    subs: [
                        {
                            index: 'drag',
                            title: '????????????'
                        },
                        {
                            index: 'dialog',
                            title: '????????????'
                        }
                    ]
                },
                {
                    icon: 'el-icon-lx-global',
                    index: 'i18n',
                    title: '???????????????'
                },
                {
                    icon: 'el-icon-lx-warn',
                    index: '7',
                    title: '????????????',
                    subs: [
                        {
                            index: 'permission',
                            title: '????????????'
                        },
                        {
                            index: '404',
                            title: '404??????'
                        }
                    ]
                },
                {
                    icon: 'el-icon-lx-redpacket_fill',
                    index: '/donate',
                    title: '????????????'
                }
            ]
        };
    },
    computed: {
        onRoutes() {
            return this.$route.path.replace('/', '');
        }
    },
    created() {
        // ?????? Event Bus ??????????????????????????????????????????
        bus.$on('collapse', msg => {
            this.collapse = msg;
            bus.$emit('collapse-content', msg);
        });
    }
};
</script>

<style scoped>
.sidebar {
    display: block;
    position: absolute;
    left: 0;
    top: 70px;
    bottom: 0;
    overflow-y: scroll;
}
.sidebar::-webkit-scrollbar {
    width: 0;
}
.sidebar-el-menu:not(.el-menu--collapse) {
    width: 250px;
}
.sidebar > ul {
    height: 100%;
}
</style>

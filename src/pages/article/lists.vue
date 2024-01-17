<script setup lang='ts'>
import { articleStore, userStore } from '@/stores'
import { cusConfirm, getTimer } from '@/utils'
import { ElMessage } from 'element-plus'
const props = defineProps<{
    articles: ArticleType[]
}>()
const store = articleStore()
</script>

<template>
    <div class="argicle-lists">
        <div class="arts-item" v-for="item in props.articles" @click="toEetail(item)">
            <div class="art-meta fx">
                {{ item.user.username }} <i /> {{ getTimer(item.created_at) }}<i />{{ store.getCateLabel(item.category) }}
            </div>
            <div class="artctx-wrapper">
                <div class="info-wrap">
                    <h3>{{ item.title }}</h3>
                    <p>{{ item.intro }}</p>
                    <div class="handle fx">
                        <span class="row">
                            <span class="iconfont icon-liulan"></span>
                            {{ item.page_view }}
                        </span>
                        <span class="row zan">
                            <span class="iconfont icon-zan"></span>
                            {{ item.praises || '点赞' }}
                        </span>
                        <span class="row">
                            <span class="iconfont icon-wenda"></span>
                            {{ item.comments || '评论' }}
                        </span>
                        <el-dropdown v-if="item.user?._id == ustore.user_info?._id"></el-dropdown>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang='less'></style>
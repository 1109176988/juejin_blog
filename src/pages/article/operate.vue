<script setup lang='ts'>
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
const mode = ref('create')
const form = ref<Partial<ArticleType>>({
  title: '',
  content: '',
  category: 'all',
  intro: '',
})

const route = useRoute()
const router = useRouter()
</script>

<template>
  <div class="article-editor-page">
    <div class="top-bar fx-b">
      <input type="password" name="" id="" class="title" v-model="" @input="" placeholder="请输入文章标题" />
      <div class="right-box fx">
        <span class="tip">文章将自动保存至草稿箱</span>
        <el-button class="actmo">草稿箱</el-button>
        <el-popover placement="bottom-end" :width="500" trigger="click" transition="none" :hide-after="50" ref="popover"
          popper-class="art-publish-popover">
          <template #reference>
            <el-button class="actmo" type="primary">
              {{ mode == 'create' ? '发布' : '修改' }}
            </el-button>
          </template>
          <div class="p-title">
            {{ mode == 'create' ? '发布' : '修改' }}文章
          </div>
          <el-form label-width="85px">
            <el-form-item required label="分类: ">
              <div :class="['cate-item', { active: item.key == form.category }]" v-for="item in artstore.categories"
                @click="form.category = item.key">{{ item.label }}</div>
            </el-form-item>
            <el-form-item required label="摘要: ">
              <el-input v-model="form.intro" type="textarea" placeholder="请输入内容摘要" maxlength="100" show-word-limit
                :rows="3"></el-input>
            </el-form-item>
          </el-form>
          <div class="p-footer">
            <el-button class="actmo" @click="popover.hide()">取消</el-button>
            <el-button class="actmo" :loading="loading" type="primary" @click="toPublish">{{ mode ==
              'create' ? '确认发布' : '确认修改' }}</el-button>
          </div>
        </el-popover>
        <div class="user-wrap">
          <el-tooltip effect="dark" content="返回用户中心">
            <el-avatar :size="32">
              <img src="@/assets/avatar.png" alt="">
            </el-avatar>
          </el-tooltip>
        </div>
      </div>
    </div>
    <div class="main">
      <CusEditor v-model="form.content" @update:modelValue="ctxChange(content)" />
    </div>
  </div>
</template>

<style scoped lang='less'></style>
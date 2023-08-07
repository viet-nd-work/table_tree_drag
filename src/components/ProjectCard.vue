<script setup>
import { ref } from "vue";
import TaskCard from "./TaskCard.vue";

const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
});

const isShowProject = ref(false);
</script>

<template>
  <div
    :class="[
      'mpj_l_b_project_table flex member_tag',
      isShowProject ? 'show_project' : '',
    ]"
  >
    <ul class="grid grid-cols-15">
      <li class="col-span-6 flex center justify-content-start des_name">
        <div class="mpj_l_b_p_t_project_name flex">
          <div
            v-if="data.tasks.length"
            class="mpj_l_b_p_t_btn_arrow flex center pr"
            @click="isShowProject = !isShowProject"
          >
            <i
              :class="[
                'fa-solid',
                isShowProject ? 'fa-caret-down' : 'fa-caret-right',
              ]"
            ></i>
          </div>
          <span
            class="text-ellipsis text-ellipsis-1 mpj_l_b_pn_title flex center"
            @click="data.tasks.length && (isShowProject = !isShowProject)"
          >
            {{ data.name }}
          </span>
          <div class="mpj_l_b_pn_btn_config flex center">
            <div class="mpj_l_b_pn_group_add_pj flex center">
              <template v-if="data.tasks.length">
                <i class="fa-solid fa-retweet mr-1"></i>
                <span class="flex center"> {{ data.tasks.length }} </span>
                <span class="flex center"> | </span>
              </template>
              <i
                class="fa-solid fa-plus mpj_l_b_p_t_btn_add_pj"
                style="color: #b0b0b0"
              ></i>
            </div>
          </div>
        </div>
      </li>
      <li class="col-span-3 flex center des_assign">
        <div class="mpj_l_b_p_t_project_assign flex center">avatar</div>
      </li>
      <li class="col-span-2 flex center des_deadline">
        <div class="mpj_l_b_p_t_project_deadline flex center"></div>
      </li>
      <li class="col-span-2 flex center des_progress"></li>
      <li class="col-span-2 flex center des_priority">
        <div class="mpj_l_b_p_t_project_priority flex center">
          <span></span>
        </div>
      </li>
    </ul>
  </div>
  <task-card
    v-for="(item, index) in data.tasks"
    :key="index"
    :is-show-parent="isShowProject"
    :data="item"
    :project-name="data.name"
    :members="data.members"
  />
</template>

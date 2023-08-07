<script setup>
import { ref } from "vue";

const props = defineProps({
  isShowParent: Boolean,
  data: {
    type: Object,
    required: true,
  },
  projectName: {
    type: String,
    required: true,
  },
  members: {
    type: Array,
    required: true,
  },
  parentName: {
    type: String,
    default: "",
  },
  oldParent: {
    type: Number,
    default: 0,
  },
});

const isShowTask = ref(false);
</script>

<template>
  <div
    draggable
    v-show="isShowParent"
    :class="['mpj_l_b_task_table flex pr', isShowTask ? 'show_task' : '']"
  >
    <div class="drag_task flex center">
      <i class="fa-solid fa-grip-vertical"></i>
    </div>
    <ul class="grid grid-cols-15">
      <li class="col-span-6 flex center justify-content-start des_name">
        <div class="mpj_l_b_t_t_task_name flex des_name">
          <div
            v-if="data.sub_task?.length"
            class="mpj_l_b_t_t_btn_arrow flex center pr"
            @click="isShowTask = !isShowTask"
          >
            <i
              :class="[
                'fa-solid',
                isShowTask ? 'fa-caret-down' : 'fa-caret-right',
              ]"
            ></i>
          </div>
          <div class="mpj_l_b_t_t_tag_priority mr-2">
            {{ data.status_id }}
          </div>
          {{ data.task_name }}
          <div class="mpj_l_b_pn_btn_config flex center">
            <div
              v-if="data.sub_task?.length || data.hasChild"
              class="mpj_l_b_tt_group_add_pj flex center"
            >
              <template v-if="data.sub_task?.length">
                <i class="fa-solid fa-retweet mr-1"></i>
                <span class="flex center">
                  {{ data.sub_task?.length || 0 }}
                </span>
                <span class="flex center"> | </span>
              </template>
              <i
                v-if="data.hasChild"
                class="fa-solid fa-plus mpj_l_b_p_t_btn_add_pj"
                style="color: #b0b0b0"
              ></i>
            </div>
            <a
              href="javascript:void(0)"
              class="flex center"
              @click="handleEditTask"
            >
              <i class="fa-solid fa-pen"></i>
            </a>
            <a href="javascript:void(0)" class="flex center">
              <i class="fa-solid fa-trash"></i>
            </a>
          </div>
        </div>
      </li>
      <li class="col-span-3 flex center des_assign">
        <div class="mpj_l_b_p_t_project_assign des_assign flex center">
          avatar
        </div>
      </li>
      <li class="col-span-2 flex center des_deadline">
        <div class="mpj_l_b_p_t_project_deadline des_deadline flex center">
          <span>
            {{ data.due_date }}
          </span>
        </div>
      </li>
      <li class="col-span-2 flex center des_progress">
        {{ data.done_ratio }}
      </li>
      <li class="col-span-2 flex center des_priority">
        <div class="mpj_l_b_p_t_project_priority des_priority flex center">
          {{ data.priority_id }}
        </div>
      </li>
    </ul>
    <task-card
      v-for="(item, index) in data.sub_task"
      :key="index"
      :is-show-parent="isShowTask"
      :data="item"
      :project-name="projectName"
      :members="data.task_members"
      :parent-name="data.task_name"
      :old-parent="data.id"
    />
  </div>
</template>

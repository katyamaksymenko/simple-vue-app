<!-- use Playground.vue to play around with the gantt chart components and test out new features -->
<template>
  <div>
   
    <g-gantt-chart
        :chart-start="chartStart"
        :chart-end="chartEnd"
        :grid="grid"
        :hide-timeaxis="hideTimeaxis"
        :push-on-overlap="false"
        snap-back-on-overlap
        :highlighted-hours="highlightedHours"
        :row-label-width="`${rowLabelWidth}%`"
        :row-height="rowHeight"
        :theme="selectedTheme"
      >
        <template v-for="(row, index) in rowList">
          <div style="width: 100%; padding: 5px; background: white;" :key="`div${row.label}`">
            test
          </div>
          <g-gantt-row
            v-on:show-task-form="showTaskForm(index)"
            v-on:edit-task="showEditTaskForm($event, index)"
            :index="index"
            :key="row.label"
            :label="row.label"
            :bars="row.barList"
            :highlight-on-hover="highlightOnHover"
            bar-start="myStart"
            bar-end="myEnd"
          >
            <template #bar-label="{bar}">
              <span>{{bar.label}}</span>
            </template>
          </g-gantt-row>
        </template>
        
      </g-gantt-chart>
      <g-gantt-task-form
        v-if="isShowTaskForm"
        v-on:add-task="addTask"
        :rowIndex="rowIndex"
        :task="task"
      ></g-gantt-task-form>
  </div>
</template>

<script>
import GGanttChart from './GGanttChart.vue'
import GGanttRow from './GGanttRow.vue'
import GGanttTaskForm from './GGanttEventForm.vue'
export default {
  components:{
    GGanttChart,
    GGanttRow,
    GGanttTaskForm
  },
  mounted() {
    if (localStorage.rowList) {
      this.rowList = JSON.parse(localStorage.rowList);
    }
  },
  watch: {
    rowList: {
      handler: function (newRowList) { localStorage.rowList = JSON.stringify(newRowList) },
      deep: true
    }
  },
  methods: {
    addTask(rowIndex, data) {
      this.rowList[rowIndex].barList.push(data);
      this.isShowTaskForm = false;
      this.rowIndex = null;
      this.taskIndex = null;
    },
    showTaskForm(rowIndex) {
      this.isShowTaskForm = true;
      this.rowIndex = rowIndex;
    },
    showEditTaskForm(taskIndex, rowIndex) {
      this.showTaskForm(rowIndex);
      this.task = this.rowList[rowIndex].barList[taskIndex];
    }
  },
  data(){
    return {
      isShowTaskForm: false,
      rowIndex: null,
      task: null,
      chartStart: "2020-03-02 00:00",
      chartEnd: "2020-03-04 00:00",
      pushOnOverlap: true,
      grid: true,
      rowHeight: 40,
      rowLabelWidth: 15,
      hideTimeaxis: false,
      highlightOnHover: false,
      hours: [...Array(24).keys()],
      highlightedHours: [10,12],
      showContextmenu: false,
      contextmenuTimeout: null,
      contextmenuX: 0,
      contextmenuY: 0,
      selectedTheme: "default",
      themes: [
        "default",
        "vue",
        "dark",
        "material-blue",
        "creamy",
        "slumber",
        "sky",
        "crimson",
        "grove",
        "fuchsia",
        "flare"
      ],
      rowList: [
        {
          label: "Row #1",
          barList: []
        },
        {
          label: "Row #2",
          barList: []
        },
        {
          label: "Row #3",
          barList: []
        },
        {
          label: "Row #4",
          barList: []
        }
      ]
    }
  }
}
</script>

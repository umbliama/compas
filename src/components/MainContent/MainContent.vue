<template>
  <main class="main">
    <h2>Проведение ТО и мелкий ремонт</h2>
    <div class="main-options">
      <div class="main-options-values">
        <a class="main-options-values__link link" href="">Общее</a>
        <a class="main-options-values__link link" href="">Товар списания</a>
        <a class="main-options-values__link link" href="">Доп. расходы</a>
      </div>
      <div class="main-options-settings" @click="dropdownOpen = !dropdownOpen">
        <img src="@/assets/options.svg" alt="" />
        <div v-if="dropdownOpen" class="main-options-dropdown">
          <div class="main-options-dropdown__item">Отображение столбцов</div>
          <div class="main-options-dropdown__item">Порядок столбцов</div>
        </div>
      </div>
    </div>
    <div class="main-newrow">
      <a href="" @click.prevent="addRow()" class="main-newrow-link link">
        <img class="main-newrow-link__img" src="@/assets/plus.svg" alt="" />
        <span class="main-newrow-link__span">Добавить строку</span>
      </a>
    </div>
    <div class="table-container">
      <table class="table">
        <thead>
          <tr>
            <th
              v-for="(column, index) in columns"
              :key="index"
              :style="{ width: column.width + 'px' }"
            >
              {{ column.title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in rows" :key="rowIndex">
            <td
              v-for="(column, colIndex) in columns"
              :key="colIndex"
              :style="{ width: column.width + 'px' }"
            >
              <div
                class="resize-trigger"
                @mousedown="startResize(colIndex, rowIndex)"
              ></div>
              <div>{{ row[column.field] }}</div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>


<script>
export default {
  data() {
    return {
      dropdownOpen: false,
      columns: [
        { title: "Column 1", field: "col1", width: 100 },
        { title: "Column 2", field: "col2", width: 150 },
        { title: "Column 3", field: "col3", width: 200 },
        { title: "Column 4", field: "col4", width: 120 },
        { title: "Column 5", field: "col5", width: 180 },
      ],
      rows: [
        {
          col1: "Row 1, Column 1",
          col2: "Row 1, Column 2",
          col3: "Row 1, Column 3",
          col4: "Row 1, Column 4",
          col5: "Row 1, Column 5",
        },
        {
          col1: "Row 2, Column 1",
          col2: "Row 2, Column 2",
          col3: "Row 2, Column 3",
          col4: "Row 2, Column 4",
          col5: "Row 2, Column 5",
        },
        {
          col1: "Row 3, Column 1",
          col2: "Row 3, Column 2",
          col3: "Row 3, Column 3",
          col4: "Row 3, Column 4",
          col5: "Row 3, Column 5",
        },
      ],
      resizeIndex: -1,
      resizeStartX: 0,
      initialWidths: [],
    };
  },
  mounted() {
    window.addEventListener("mousemove", this.handleResize);
    window.addEventListener("mouseup", this.stopResize);
  },
  methods: {
    startResize(index) {
      this.resizeIndex = index;
      this.resizeStartX = event.clientX;
      this.initialWidths = this.columns.map((column) => column.width);
    },
    handleResize(event) {
      if (this.resizeIndex === -1) return;
      const deltaX = event.clientX - this.resizeStartX;
      const newWidth = this.initialWidths[this.resizeIndex] + deltaX;
      if (newWidth > 0) {
        // Use Vue.set to update the property value for reactivity
        this.columns[this.resizeIndex] = {
          ...this.columns[this.resizeIndex],
          width: newWidth,
        };
      }
    },
    stopResize() {
      this.resizeIndex = -1;
    },
    openDropdown() {
      this.dropdownOpen = !this.dropdownOpen;
    },
    addRow() {
      const newRow = {
        // Define the properties of the new row object here
        // For example:
        name: "",
        date: "",
        price: 0,
      };
      this.rows.push(newRow);
    },
  },
};
</script>



<style lang="scss" scoped>
.main {
  margin: 0 0 0 25px;
  color: #000;
  &-options {
    margin: 25px 0;
    display: flex;
    justify-content: space-between;
    &-dropdown {
      position: absolute;
      top: 40px;
      right: 0;
      width: 200px;
      border: 1px solid #ccc;
      background-color: #fff;
      z-index: 1;
      &__item {
        padding: 8px 12px;
        cursor: pointer;
        &:hover {
          background-color: #f2f2f2;
        }
      }
    }
    &-values {
      &__link {
        margin: 0 20px 0 0;
      }
    }
  }
  &-newrow {
    padding: 20px 0 20px 25px;
    border-radius: 10px;
    box-shadow: 0 5px 20px 0 rgba(0, 0, 0, 0.07);
    border: solid 1px #eeeff1;
    background-color: var(--white);
    margin: 0 0 25px 0;
    &-link {
      padding: 10px 15px 10px 10px;

      border-radius: 5px;

      background-color: #2f8cff;
      &__span {
        color: #fff;
      }
      &__img {
        margin: 0 7px 0 0;
      }
    }
  }
}
.table-container {
  overflow-x: auto;
}

.table {
  table-layout: fixed;
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}

.resize-trigger {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  width: 4px;
  cursor: col-resize;
}
</style>

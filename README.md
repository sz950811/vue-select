## 效果图
![image](https://github.com/sz950811/vue-select/assets/64963500/86103624-7eff-4f0d-adf0-53906adefdf1)

## 页面结构

```html
  <el-select
      v-model="dataRepresentationValue"
      :popper-class="'mySelect'"
      :multiple="true"
      collapse-tags
    >
      <el-option
        v-for="(item, i) in dataRepresentation"
        :key="item.label"
        :label="item.label"
        :value="item.id"
      >
        <!--  dom结构区域 -->
        <div class="box">
          <el-row>
            <el-col :span="3" class="page-lv3-title" @click.stop.native>{{
              item.label
            }}</el-col>
            <el-col :span="21" style="text-align: right">
              <el-button
                class="custom"
                :type="item.buttonShow === 1 ? 'primary' : 'text'"
                @click.stop="rangeSelection(null, null, 1, i)"
                >不限</el-button
              >

              <el-button
                class="custom"
                :type="item.buttonShow === 2 ? 'primary' : 'text'"
                @click.stop="rangeSelection(0, 100, 2, i)"
                >&lt;100</el-button
              >
              <el-button
                class="custom"
                :type="item.buttonShow === 3 ? 'primary' : 'text'"
                @click.stop="rangeSelection(100, 1000, 3, i)"
                >100-1k</el-button
              >
              <el-button
                class="custom"
                :type="item.buttonShow === 4 ? 'primary' : 'text'"
                @click.stop="rangeSelection(1000, 10000, 4, i)"
                >1k-1w</el-button
              >
              <el-button
                class="custom"
                :type="item.buttonShow === 5 ? 'primary' : 'text'"
                @click.stop="rangeSelection(10000, 100000, 5, i)"
                >1w-10w</el-button
              >
              <el-button
                class="custom"
                :type="item.buttonShow === 6 ? 'primary' : 'text'"
                @click.stop="rangeSelection(100000, null, 6, i)"
                >&gt;10w</el-button
              >
              <el-button
                :type="item.buttonShow === 7 ? 'primary' : 'text'"
                @click.stop="rangeSelection(null, null, 7, i)"
                class="custom"
                >自定义</el-button
              >
            </el-col>
          </el-row>
          <el-row
            class="input-box"
            v-show="item.buttonShow === 7 && item.customShow"
          >
            <el-col :span="8">
              <el-input
                @click.stop.native
                v-model.number.trim="filterConfig.dataRepresentation[i].min"
              ></el-input>
            </el-col>
            <el-col :span="2" style="text-align: center">
              <div>to</div>
            </el-col>
            <el-col :span="8">
              <el-input
                @click.stop.native
                v-model.number.trim="filterConfig.dataRepresentation[i].max"
              ></el-input>
            </el-col>
            <el-col :span="6">
              <el-button @click.stop="onRefreshInput(i)" class="custom"
                >重置</el-button
              ><el-button
                v-show="false"
                type="primary"
                @click.stop="customConfirm(i)"
                class="custom"
                >确定</el-button
              >
            </el-col>
          </el-row>
        </div>
      </el-option>
    </el-select>
```

## 定义所需数据格式

```javascript
 dataRepresentationValue: [1, 2, 3, 4, 5],
      dataRepresentation: [
        {
          label: "分享数",
          id: 1,
          customShow: false, // 自定义输入框显示隐藏
          buttonShow: 1, // 文字按钮与默认按钮切换
        },
        {
          label: "评论数",
          id: 2,
          customShow: false,
          buttonShow: 1,
        },
        {
          label: "点赞数",
          id: 3,
          customShow: false,
          buttonShow: 1,
        },
        {
          label: "收藏数",
          id: 4,
          customShow: false,
          buttonShow: 1,
        },
        {
          label: "粉丝数",
          id: 5,
          customShow: false,
          buttonShow: 1,
        },
      ],
      filterConfig: {
        dataRepresentation: [
          {
            type: 1,
            min: null,
            max: null,
          },
          {
            type: 2,
            min: null,
            max: null,
          },
          {
            type: 3,
            min: null,
            max: null,
          },
          {
            type: 4,
            min: null,
            max: null,
          },
          {
            type: 5,
            min: null,
            max: null,
          },
        ],
      },
```

## 功能实现

```javascript
    /**
     * min 最小值 max 最大值 show 按钮样式切换 i 元素下标
     */
    rangeSelection(min, max, show, i) {
      this.dataRepresentation[i].buttonShow = show;
      this.dataRepresentation[i].customShow = true;
      this.filterConfig.dataRepresentation[i].min = min;
      this.filterConfig.dataRepresentation[i].max = max;
    },
    // 打开自定义输入框
    customConfirm(i) {
      this.dataRepresentation[i].customShow = true;
    },
    // 重制输入框
    onRefreshInput(i) {
      this.filterConfig.dataRepresentation[i].min = null;
      this.filterConfig.dataRepresentation[i].max = null;
    },
```


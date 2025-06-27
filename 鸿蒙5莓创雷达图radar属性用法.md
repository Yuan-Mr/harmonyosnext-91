大家好，欢迎回来鸿蒙5莓创图表组件的专场，我们这一期来讲解雷达图（McRadarChart）的核心配置属性——radar属性的详细用法。我们将通过「作用+类型+默认值+可选值+场景+代码示例」的维度，深度剖析每个属性及其子属性的完整配置方案。

* * *

### 一、indicator属性

作用：定义雷达图的维度指标（即雷达图“顶点”对应的变量名称和最大值） 类型：`Array<{name: string, max?: number}>` 默认值：`[]`（空数组） 可选值：每个对象必须包含`name`属性，可选`max`定义该维度最大值 场景：需要展示多维数据对比时使用（如技能评分、性能参数等）

```
radar: {
  indicator: [
    {name: '鸿蒙', max: 1500},  // 自定义最大值
    {name: 'ios'},             // 默认最大值由数据自动推算
    {name: '安卓'},
    {name: 'Magic'}
  ]
}
```

* * *

### 二、center属性

作用：设置雷达图的圆心坐标 类型：`Array<string>` 默认值：`["50%", "50%"]`（页面居中） 可选值：百分比字符串（如`"40%"`）或具体像素值（如`"200px"`） 场景：需要调整雷达图在容器中的位置时使用

```
radar: {
  center: ["30%", "60%"],  // 横向30%位置，纵向60%位置
  radius: "40%"
}
```

* * *

### 三、radius属性

作用：控制雷达图的半径大小 类型：`string | number` 默认值：`"65%"` 可选值：百分比字符串（适配容器）或具体像素数值 场景：需要适配不同屏幕尺寸或调整图表占比时

```
radar: {
  radius: "80%",  // 占容器80%宽度
  // radius: 300   // 固定像素值
}
```

* * *

### 四、startAngle属性

作用：设置坐标系起始旋转角度 类型：`number` 默认值：`-Math.PI / 2`（-90度，12点钟方向） 可选值：弧度值（如`Math.PI/2`表示90度） 场景：需要旋转雷达图方向时使用

```
radar: {
  startAngle: 0,  // 0弧度对应3点钟方向
  indicator: [...] 
}
```

* * *

### 五、nameGap属性

作用：调整指标名称与轴线的间距 类型：`number` 默认值：`10` 可选值：任意正整数 场景：指标名称过长需要调整布局时

```
radar: {
  nameGap: 20,
  axisName: { fontSize: 18 }
}
```

* * *

### 六、splitNumber属性

作用：设置坐标轴分割段数 类型：`number` 默认值：`5` 可选值：大于1的正整数 场景：控制网格密度，数值越大网格越密集

```
radar: {
  splitNumber: 8,  // 生成8层同心圆网格
  splitArea: { show: true }
}
```

* * *

### 七、polygon属性

作用：切换多边形/圆形雷达图模式 类型：`boolean` 默认值：`true`（多边形） 可选值：`true`|`false` 场景：需要呈现不同风格的雷达图时

```
radar: {
  polygon: false,  // 启用圆形模式
  splitLine: { show: true }
}
```

* * *

### 八、axisName属性（对象属性）

作用：配置指标名称的文本样式 子属性详解：

-   show：是否显示（`boolean`，默认`true`）
-   color：文字颜色（`string`，默认`"#999"`）
-   fontSize：字号（`number`，默认`22`）
-   fontWeight：字重（`string`，默认`"normal"`）
-   overflow：超长处理（`"none"|"truncate"|"breakAll"`，默认`"truncate"`）

场景：需要个性化指标名称样式时

```
radar: {
  axisName: {
    color: "#FF5733",
    fontSize: 16,
    overflow: "breakAll",
    width: 40  // 最大文本宽度
  }
}
```

* * *

### 九、axisLine属性（对象属性）

作用：配置坐标轴轴线样式 子属性详解：

-   show：是否显示轴线（`boolean`，默认`false`）
-   lineStyle.color：轴线颜色（`string`，默认`"#DBDBDB"`）
-   lineStyle.width：轴线宽度（`number`，默认`1`）

场景：需要强调坐标轴轮廓时

```
radar: {
  axisLine: {
    show: true,
    lineStyle: {
      color: "#4A90E2",
      width: 2
    }
  }
}
```

* * *

### 十、splitArea属性（对象属性）

作用：配置网格背景区域样式 子属性详解：

-   show：是否显示（`boolean`，默认`true`）
-   areaStyle.colors：渐变色数组（`string[]`，默认`["#fff","#ff2f5af3"]`）

场景：需要增强图表层次感时

```
radar: {
  splitArea: {
    show: true,
    areaStyle: {
      colors: ["rgba(255,99,71,0.1)", "rgba(60,179,113,0.1)"]
    }
  }
}
```

* * *

### 实战案例：产品竞争力分析仪表盘

```
@Entry
@Component
struct ProductAnalysis {
  @State option: Options = new Options({
    radar: {
      indicator: [
        {name: '用户体验', max: 100},
        {name: '性能指标'},
        {name: '市场份额'},
        {name: '研发投入'},
        {name: '生态建设'}
      ],
      center: ["55%", "45%"],
      radius: "75%",
      startAngle: 45,
      splitNumber: 6,
      axisName: {
        color: "#2c3e50",
        fontSize: 14,
        fontWeight: "bold"
      },
      splitArea: {
        areaStyle: {colors: ["#f8f9fa", "#e9ecef"]}
      }
    },
    series: [{
      name: '竞品A',
      data: [85, 78, 92, 65, 88],
      areaStyle: {color: ["#296DFF", "#296DFF33"]}
    }]
  })

  build() {
    Row() {
      McRadarChart({options: this.option})
    }.height('60%')
  }
}
```

该案例通过组合使用：

-   `startAngle`旋转45度提升视觉新颖度
-   自定义`splitArea`背景色增强可读性
-   精准设置`max`值实现标准化对比
-   半透明渐变色区域提升层次感

* * *

好，这期讲到这里就结束了，希望大家通过这篇深度解析，能熟练掌握雷达图的核心配置技巧。在实际开发中，建议先规划好数据维度，再通过属性组合实现「数据可视化+美学表达」的双重目标。遇到复杂场景时，善用对象型属性的细粒度控制能力，打造专业级数据看板！我们下期再见！
### Hello everyone, welcome back to our special session on HarmonyOS 5 Berry Creative chart components. In this episode, we'll explore the core configuration property of the radar chart (McRadarChart): the detailed usage of the **radar** property. We'll dissect each attribute and its sub-properties through the dimensions of **Function + Type + Default Value + Options + Scenarios + Code Examples**.  


### 一、`indicator` Property  
**Function**: Define dimensional indicators (variable names and maximum values for radar chart "vertices").  
**Type**: `Array<{name: string, max?: number}>`  
**Default**: `[]` (empty array)  
**Options**: Each object must include `name`; `max` is optional to define the dimension's maximum value.  
**Scenario**: Display multi-dimensional data comparisons (e.g., skill scores, performance metrics).  

```json
radar: {
  indicator: [
    {name: 'HarmonyOS', max: 1500},  // Custom maximum
    {name: 'iOS'},                   // Maximum auto-calculated from data
    {name: 'Android'},
    {name: 'Magic'}
  ]
}
```  


### 二、`center` Property  
**Function**: Set the radar chart's center coordinates.  
**Type**: `Array<string>`  
**Default**: `["50%", "50%"]` (centered)  
**Options**: Percentage strings (e.g., `"40%"`) or pixel values (e.g., `"200px"`).  
**Scenario**: Adjust chart position within the container.  

```json
radar: {
  center: ["30%", "60%"],  // 30% horizontal, 60% vertical
  radius: "40%"
}
```  


### 三、`radius` Property  
**Function**: Control the radar chart's radius.  
**Type**: `string | number`  
**Default**: `"65%"`  
**Options**: Percentage (relative to container) or pixel value.  
**Scenario**: Adapt to different screen sizes or adjust chart proportions.  

```json
radar: {
  radius: "80%",  // 80% of container width
  // radius: 300   // Fixed pixel value
}
```  


### 四、`startAngle` Property  
**Function**: Set the starting rotation angle of the coordinate system.  
**Type**: `number`  
**Default**: `-Math.PI / 2` (-90 degrees, 12 o'clock)  
**Options**: Radian values (e.g., `Math.PI/2` for 90 degrees).  
**Scenario**: Rotate the radar chart direction.  

```json
radar: {
  startAngle: 0,  // 0 radians (3 o'clock)
  indicator: [...] 
}
```  


### 五、`nameGap` Property  
**Function**: Adjust spacing between indicator names and axes.  
**Type**: `number`  
**Default**: `10`  
**Options**: Any positive integer.  
**Scenario**: Prevent layout issues with long indicator names.  

```json
radar: {
  nameGap: 20,
  axisName: { fontSize: 18 }
}
```  


### 六、`splitNumber` Property  
**Function**: Set the number of axis divisions.  
**Type**: `number`  
**Default**: `5`  
**Options**: Positive integers greater than 1.  
**Scenario**: Control grid density (higher values create denser grids).  

```json
radar: {
  splitNumber: 8,  // 8 concentric grid layers
  splitArea: { show: true }
}
```  


### 七、`polygon` Property  
**Function**: Toggle between polygon and circular radar chart modes.  
**Type**: `boolean`  
**Default**: `true` (polygon)  
**Options**: `true` | `false`  
**Scenario**: Choose different visual styles.  

```json
radar: {
  polygon: false,  // Enable circular mode
  splitLine: { show: true }
}
```  


### 八、`axisName` Property (Object)  
**Function**: Configure text style for indicator names.  
**Sub-properties**:  
- `show`: Visibility (`boolean`, default `true`).  
- `color`: Text color (`string`, default `"#999"`).  
- `fontSize`: Font size (`number`, default `22`).  
- `fontWeight`: Font weight (`string`, default `"normal"`).  
- `overflow`: Handling for超长 text (`"none" | "truncate" | "breakAll"`, default `"truncate"`).  

**Scenario**: Customize indicator name styles.  

```json
radar: {
  axisName: {
    color: "#FF5733",
    fontSize: 16,
    overflow: "breakAll",
    width: 40  // Maximum text width
  }
}
```  


### 九、`axisLine` Property (Object)  
**Function**: Configure axis line styles.  
**Sub-properties**:  
- `show`: Visibility (`boolean`, default `false`).  
- `lineStyle.color`: Line color (`string`, default `"#DBDBDB"`).  
- `lineStyle.width`: Line width (`number`, default `1`).  

**Scenario**: Emphasize axis outlines.  

```json
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


### 十、`splitArea` Property (Object)  
**Function**: Configure grid background area styles.  
**Sub-properties**:  
- `show`: Visibility (`boolean`, default `true`).  
- `areaStyle.colors`: Gradient color array (`string[]`, default `["#fff", "#ff2f5af3"]`).  

**Scenario**: Enhance chart depth.  

```json
radar: {
  splitArea: {
    show: true,
    areaStyle: {
      colors: ["rgba(255,99,71,0.1)", "rgba(60,179,113,0.1)"]
    }
  }
}
```  


### Practical Case: Product Competitiveness Analysis Dashboard  

```typescript
@Entry
@Component
struct ProductAnalysis {
  @State option: Options = new Options({
    radar: {
      indicator: [
        {name: 'User Experience', max: 100},
        {name: 'Performance Metrics'},
        {name: 'Market Share'},
        {name: 'R&D Investment'},
        {name: 'Ecosystem Development'}
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
      name: 'Competitor A',
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

**Key Techniques**:  
- Rotate 45° with `startAngle` for visual freshness.  
- Use custom `splitArea` colors for better readability.  
- Set precise `max` values for standardized comparisons.  
- Employ semi-transparent gradient areas for depth.  


### Conclusion  
That concludes our in-depth guide to the radar chart's core configuration! Master these techniques to create professional-grade data visualizations. In practice, plan your data dimensions first, then combine properties to achieve both **data clarity** and **aesthetic appeal**. Leverage object-based properties for granular control in complex scenarios. See you next time! 📊

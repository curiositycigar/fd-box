## 安装
> npm install fd-box --save
## 使用
#### javascript
```
import box from 'fd-box';

export default {
  data() {
    header: true, // true&false, 是否显示header,默认true
    title: 'I\'m header', // header中的文字
    width: '500px', // 盒子宽度，默认100%
    height: '300px', // 盒子高度，默认 300px
    type: 'stylename', //header图标类型 clock message setting warning error cancel disabled
    bars: [1,2], // 分栏条数 传递数组，如[1,2],按数组内容等比分栏,也可传数字，按数字平分n栏,默认数字1
    size: 'small' // tiny,small,big,large
  },
  components: {
    'yourname-box': box
  }
}
```
#### html
```
<yourname-box
  :title="title"
  :height="height"
  :width="width">
  <!-- 根据分栏数目插入数据slot name 1,2,3... -->
  <div slot='1'></div>
  <div slot='2'></div>
</yourname-box>
```

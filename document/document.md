Title         : Welcome
Author        : You
Logo          : True


[TITLE]

# Madoko 

Madoko is a fast markdown processor for writing professional articles
with a focus on simplicity and plain text readability.

* Read the [reference manual].
* Explore the upper-right toolbox menu to discover how Markdown works. 
* `Alt-Q` reformats the current paragraph.

Enjoy!

## scss 语法
### for 循环

 ```
 @for $i from 1 through 20 {
    @if($i >= 8){
      .f#${i}{
        font-size: $i * 1px
      }
    }
     .mr#{$i}{
        margin-right: ($i * 1px);
    }
    .ml#{$i}{
        margin-left: ($i * 1px);
    }
    .mt#{$i}{
        margin-bottom: ($i * 1px)
    }
    .mt#{$i}{
        margin-top: ($i * 1px);
    }
    .pt#{$i}{
        padding-top: ($i * 1px);
    }
    .pl#{$i}{
        padding-left: ($i * 1px);
    }
    .pr#{$i}{
        padding-right: ($i * 1px);
    }
    .pb#{$i}{
        padding-bottom: ($i * 1px);
    }
   }
  
```

### mixin 混淆用法

```
  @mixin flex($direction: column,$inline:flex){
    display: $inline;
    flex-direction: $direction;
    flex-wrap:nowrap
  }
  
  // 水平垂直居中
@mixin center ($direction:column){
    @include flex($direction);
    justify-content: center;
    align-items: center;
}
  ```
  
## vue中的唯一值 uid

1. 使用this._uid可以访问到当前界面的唯一值，并作为实际用途

## 创建svgIcon组件 
1. 在svg图片的目录创建index.js
```
  const requireAll = requireContext => requireContext.keys().map(requireContext)
const req = require.context('./svg', true, /\.svg$/)
requireAll(req)
  ```
2. 下载svg-sprite-loader@4.1.3
3. 修改vue.config.js
```
  chainWebpack:config => {
    const svgRule = config.module.rule('svg')
    // 清除已有的所有 loader,如果你不这样做，接下来的 loader 会附加在该规则现有的 loader 之后。
    svgRule.uses.clear()
    // 添加要替换的 loader
    svgRule
    .test(/\.(svg)(\?.*)?$/)
    .exclude
    .add(/node_modules/) // 正则匹配排除node_modules目录
    .end()
    .use('svg-sprite-loader')
    .loader('svg-sprite-loader')
    .options({
      symbolId: 'icon-[name]'
    })
  }
  重启项目
  ```
4. 创建组件 SvgIcon.svg
  ```
    <template>
  <svg  class="svg-icon" :class="svgClass" aria-hidden="true">
    <use :xlink:href="iconName"></use>
  </svg>
</template>
<script>
export default {
  name: 'svg-icon',
  props: {
    iconClass: {
      type: String
    },
    className: {
      type: String
    }
  },
  computed: {
    iconName () {
      return `#icon-${this.iconClass}`
    },
    svgClass () {
      if (this.className) {
        return `svg-icon ${this.className}`
      }
      return `svg-icon`
    }
  }
}
</script>
<style lang="scss" scoped>
.svg-icon {
  width: 16px;
  height: 16px;
  vertical-align: middle;
  fill: currentColor;
  overflow: hidden;
}
</style>
    ```
    
5. main.js 引入组件 还有svg目录下的index.js
   vue3在main.js中全局注册组件 
   ```
    import '@/assets/index.js'
// 注册svgicon
import SvgIcon from '@/components/SvgIcon.vue'
const app = createApp(App)
app.component('svg-icon', SvgIcon)
     ```


6. 下载第三方 使用方法
```

export function MP(ak) {
  return new Promise((resolve, reject) => {
    // 如果已加载直接返回
    if (typeof BMapGL !== 'undefined') {
      resolve(BMapGL)
      return true
    }
    // 百度地图异步加载回调处理
    window.BMapGLInit = function() {
      // console.log("百度地图脚本初始化成功...");
      resolve(BMapGL)
    }

    // 插入script脚本
    const script = document.createElement('script')
    script.src = `//api.map.baidu.com/api?type=webgl&v=1.0&ak=843V9geCxA8cszfBfThYozGe0Q1epIsd&callback=BMapGLInit`
    document.body.appendChild(script)
  })
}
```
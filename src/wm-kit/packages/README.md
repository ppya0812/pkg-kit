#这是基于VUE实现的一款轻量级移动端组件库。

## 1. carousel 轮播组件

### 支持功能(API):

name           |     type | default |               description
-------------- | -------: | :-----: | :-------------------------------------:
loop           |  Boolean |  true   |                 是否循环播放
auto           |   Number |  3000   | 是否自动播放，0不自动播放，其他值则自动播放，值为其自动播放的interval
indicators     |  Boolean |  false  |        是否添加屏点，不带任何样式，样式可参考demo写
responsive     |   Number |   40    |  是否开启响应式高度，若为0则不开启，其他正整数表示 高度是宽度的百分之多少
flickThreshold |   Number |   0.6   |                 轻弹的最小速度
delta          |   Number |   100   |             滚动时触发滚动到下一张的最小值
onSlidEnd      | Function |  noop   |               轮播切换完成时的回调
preventDefault |  Boolean |  false  |           取消touchmove事件的默认动作

### 示例:

```
<template>
    <div class="banner-wrap">
        <carousel :indicators="true" :auto="3000" :responsive="36.533333333333334" :on-slid-end="onSlidEnd">
            <div v-for="(item, index) in banner" :key="index"></div>
        </carousel>
    </div>
</template>
<script>
    import Carousel from '../Carousel';
    export default {
        components: {
            Carousel
        },
        methods: {
            onSlidEnd() {
                // TODO: 轮播切换完成时的回调
            }
        }
    }
</script>
```


## 2. scroll 滚动组件
* 采用quadratic 、circular 、back等缓动算法，基于translate & cubic-bezier曲线实现的一款移动端轻量级滚动插件。

### 支持功能(API -- props参数):
name            |           type |  default   |                        description
--------------- | -------------: | :--------: | :--------------------------------------------------------:
scrollDirection |         string | horizontal |                 滚动方向(horizontal/vertical)
refreshStatus   |Boolean, Number |            |                 判断是否需要重新更新组件
scrollToEle     | HTMLDivElement | undefined  |             滚动列表特定元素的domevent(activeEvent： '')
activeTargetPos |         String |   center   | 所传入的滚动DOM的位置(水平滚动center/left/right, 垂直滚动center/top/bottom)
moveCallback    |       Function |   i => 0   |                         滚动过程中的回调函数
moveEndback     |       Function |   i => 0   |                         滚动过程中的回调函数
afterRelease    |       Function |   i => 0   |                    列表尾部滚动完成释放touch的回调函数
beforeRelease   |       Function |   i => 0   |                    列表头部滚动完成释放touch的回调函数
beyondFn        |       Function |   i => 0   |                         滚动时超出更多时回调
cancelBeyondFn  |       Function |   i => 0   |                        滚动时取消超出更多时回调
moreShadow      |        Boolean |   false    |                  滚动至尾部是否展示阴影效果（仅对水平滑动有效）


### 使用示例

```
// xxx.vue
<template>
    <div class="XXX">
        <scroll :scrollToEle="scrollToEle" :moreShadow="moreShadow" :afterRelease="afterRelease" :beforeRelease="beforeRelease">
            <div class="category-inner">
                <div v-for="(v, i) in category" :key="v.id" @click="activeIndex" :class="['category-item', { active: v.id === activedCategory }]">
                    {{ v.name }}
                </div>
            </div>
        </scroll>
    </div>
</template>
<script>
    // * 引入
    import Scroll from 'xxx/components/Scroll';
    data() {
        return {
            scrollToEle: undefined,
            moreShadow: true, // 滚动至尾部是否展示阴影效果（仅对水平滑动有效）
            scrollDirection: 'horizontal' // (horizontal/vertical, 默认horizontal)
        };
    },
    components: {
        Scroll
    },
    methods: {
        scrollToActivedElement() {
            // 确保激活的分类在可视区域
            Vue.nextTick(() => {
                this.scrollToEle = this.$el.querySelector('.active');
            });
        },
        afterRelease() {
            console.log('afterRelease');
            // TODO: afterRelease
        },
        beforeRelease() {
            console.log('beforeRelease');
            // TODO: beforeRelease
        }
    }
</script>
```


## 3. sticky组件

### 支持功能(API -- props参数):
name            |           type     |  default   |                        description
--------------- | -------------:     | :--------: | :--------------------------------------------------------:
top             |   [Number, String] | 'auto'     |                 定位时距离顶部的距离，默认保持跟firefox的实现一致
z-ndex          |         Number     |  10        |                 css中的z-index值

### 使用示例
```
    <sticky>
        <div class="stickyed">sticky</div>
    </sticky>
    <script>
        import Sticky from 'vue-sticky-position'
        export default {
            components: {
                Sticky
            }
        }
    </script>
```

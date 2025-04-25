### 响应式数据
vue3响应式数据：需要修改的数据定义成响应式的ref reactive。
reactive包装后的对象是个proxy对象。根据proxy的特性，reactive对对象的包裹是“深层”的。
弹幕中多人说，都用ref 不用reactive.但其实用ref也是引用了reactive 层级较深时推荐reactive
reactive对象，直接修改会失去响应式。可以使用assign来复制一份新属性到原先的响应式对象。
第15课，reactive对象的属性都是“响应式”的，因为proxy拦截了属性的修改。解构的时候，则是把数据复制给了新变量，这不是响应式的。需要经过toRefs包装才能解构。使得属性单独变成ref对象。记得加.value。toRefs方法创建了一个新对象，并且每个属性的value都指向了原先对象对应的值。
16课，vue3中的计算属性。表单中的数据双向绑定是v-model，计算属性computed引入后可以直接调用。
let fullName = computed(()=>{})计算属性只读的ref的value。
let fullName = computed({get, set})可读可写
计算属性的优势是缓存。不变不需要重新计算。
watch:监视响应式数据。传入的第二个参数是回调(newvalue, oldvalue) => {}
watch可以返回一个函数，调用可以停止watch
watch监视ref包裹的对象（注意是监测整体对象），想要监测内部属性（而不是整个对象）变化，则要添加第三个参数{deep: true}
watch监视reactive类型对象时，默认深度监视。
如果要单独监视对象中某一属性的变化person.name ，需要使用函数返回person.name如果属性是一个对象，可复习20课。最好也用函数返回这个属性的形式。且开启{deep: true}
watch监视所有情况组成的数组。
watchEffect 自动监测回调中想要修改的数据
<h2 ref="title2"> ref有点类似于id，在js里创建一个同名的键。两个地方就能联系起来。且不会和其它模块里的同名标签冲突。如果使用原生的id则会冲突。
defineExpose暴露组件内的数据
import {defineProps} from 'vue' let x = defineProps(['a']) 从父组件接收特性a，保存在defineProps生成的字典里。子组件的模板里可以直接{{a}}
ts中reactive defineProps等函数可以限制元素类型<泛型>。
withDefaults()..第25课
生命周期：用onBeforeMounted之类的函数，注册一个回调函数。

### 路由
一般约定通过路由来访问的组件，放在pages或views目录下。
路由除了用字符串形式使用，还可以“对象”的形式使用。如 :to="{path: '/home'}" :to="{name: 'home'}" 后文由于涉及到params传参，应该使用name
路由下面可以添加children: [] 子路由不需要写斜杠
子路由想要渲染的位置只要写上<router-view></router-view>，即可从对应的template获得内容，template中所需的数据应在子组件的setup中返回。
在子组件的setup中调用useRoute()可获得上级路由传过来的查询参数
路由的props:true选项或props(){}复习39
40课，routerlink标签可以用replace特性。使导航不能前进后退。
useRouter().push() useRouter().replace
46使用pinia给的数据是reactive下的REf，引用时无需.value
storeToRefs 类似于torefs，但只修改部分有需要的数据。
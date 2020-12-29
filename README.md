# <p align="center"> Binding </p>

<p align="center">
One line of code implements DataBinding and ViewBinding. Welcome star<br/>
一行代码实现 DataBinding 和 ViewBinding，欢迎 star
</p>

<p align="center">
    <a href="https://github.com/hi-dhl/Binding">English</a> &nbsp;
    ·
    &nbsp;<a href="https://github.com/hi-dhl/Binding/doc/README_CN.md">中文</a>
</p>
  
<p align="center">  
    <a href="https://github.com/hi-dhl">
        <img src="https://img.shields.io/badge/GitHub-HiDhl-4BC51D.svg?style=flat">
    </a>  

    <img src="https://img.shields.io/badge/language-kotlin-orange.svg"/> 
    
    <a href="https://bintray.com/hi-dhl/MeavenCenter/libraryName-binding/1.0.7/link"><img src="https://api.bintray.com/packages/hi-dhl/MeavenCenter/libraryName-binding/images/download.svg?version=1.0.7"/></a> 
    
    <img src="https://img.shields.io/badge/platform-android-lightgrey.svg"/>
</p>

<p align="center"> If the image cannot be viewed, please click here to view it <a href="http://img.hi-dhl.com/vbdb.png"> img1 </a> | <a href="http://img.hi-dhl.com/ViewBidnding.png"> img2 </a></p>

<p align="center">
<image src="http://img.hi-dhl.com/vbdb.png" width = 600px/>
</p>

<p align="center">
<image src="http://img.hi-dhl.com/ViewBidnding.png" width = 600px/>
</p>

**Thanks**

* Thanks to Google Translation
* the idea from [Simple one-liner ViewBinding in Fragments and Activities with Kotlin](https://medium.com/@Zhuinden/simple-one-liner-viewbinding-in-fragments-and-activities-with-kotlin-961430c6c07c)
* learn skills from open source libraries such as [Anko](https://github.com/Kotlin/anko) 、 [ViewBindingDelegate](https://github.com/hoc081098/ViewBindingDelegate) and jetpack

## 关于 Binding

Binding simplifies the use of DataBinding and ViewBinding, and only requires one line of code to implement DataBinding and ViewBinding.

The future plan of Binding provides a general `findViewById` solution. Due to the iterative update of technology from butterknife, DataBinding, Kotlin synthesis method (Synthetic view) to the current ViewBinding, there may be new technologies in the future. No matter how the technology changes, just need Update Binding, the external use remains unchanged.

Kotlin synthesis method (Synthetic view) is so much more convenient than ViewBinding, why is it abandoned by Google, please check this article [Kotlin 插件的落幕，ViewBinding 的崛起](https://mp.weixin.qq.com/s/FxrRyXp9-VDdv-mfkzsIsA)。

Thank you for your suggestions. At present, Binding has been adapted to a large number of scenarios. At the same time, it also provides a lot of practical cases of DataBinding and ViewBinding. If you encounter Binding incompatible scenarios during use, please raise an issue and I will solve it as soon as possible. .

**If this repository is helpful to you, please give me star, thank you very much for your support, and welcome you to submit a PR** ❤️❤️❤️

**[Binding](https://github.com/hi-dhl/Binding)  the following advantages：**

* A simple API requires only one line of code to implement DataBinding or ViewBinding
* Support the use of DataBinding or ViewBinding in the `Activity` 、`AppCompatActivity` 、`FragmentActivity` 、`Fragment` 、`Dialog` 
* Support the use of DataBinding or ViewBinding in the `ListAdapter` 、 `PagingDataAdapter` 、 `RecyclerView.Adapter` 
* Support the use of DataBinding and ViewBinding in Navigaion Fragment management framework, BottomSheetDialogFragment and other scenarios
* Avoid a lot of template code
* Avoid memory leaks, have life cycle awareness, and automatically destroy data when the life cycle is in `onDestroyed()`

## Download

**add jcenter**

Add the following code to the `build.gradle` file at the Project level

```
allprojects {
    repositories {
        jcenter()
    }
}
```

**add dependency**

Add the following code to the module level `build.gradle` file, and you need to enable DataBinding or ViewBinding

```
android {
    buildFeatures {
        dataBinding = true
        viewBinding = true
    }
}

dependencies {
    implementation 'com.hi-dhl:binding:1.0.7'
}
```


## Usage

* Use DataBinding and ViewBinding in Adapter (ListAdapter, PagingDataAdapter, RecyclerView.Adapter, etc.), add `by viewbind()` or `by databind()`, the example is as follows，[see example](https://github.com/hi-dhl/Binding/blob/main/app/src/main/java/com/hi/dhl/demo/binding/databind/list/ProductAdapter.kt)

```
class ProductViewHolder(view: View) : RecyclerView.ViewHolder(view) {
    
    // DataBinding
    val binding: RecycleItemProductBinding by databind()

    fun bindData(data: Product?, position: Int) {
        binding.apply {
            product = data
            executePendingBindings()
        }
    }
}

class ProductViewHolderHeader(view: View) : RecyclerView.ViewHolder(view) {

    // ViewBinding
    val binding: RecycleItemProductHeaderBinding by viewbind()

    fun bindData(data: Product?, position: Int) {
        binding.apply {
            name.text = "通过 ViewBinding 绑定的 head"
        }
    }
}

class ProductViewHolderFooter(view: View) : RecyclerView.ViewHolder(view) {
    
    // ViewBinding
    val binding: RecycleItemProductFooterBinding by viewbind()

    fun bindData(data: Product?, position: Int) {
        binding.apply {
            name.text = "通过 ViewBinding 绑定的 footer"
        }
    }
}

```

* use in `Activity`, `AppCompatActivity`, and `FragmentActivity`, add `by viewbind()` or `by databind(R.layout.activity_main)`, the example is as follows.

```
class MainActivity : AppCompatActivity() {

    // DataBinding
    val binding: ActivityMainBinding by databind(R.layout.activity_main)
    
    // ViewBinding
    val binding: ActivityMainBinding by viewbind()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding.apply {
            textView.setText("Binding")
        }
    }
}

class MainActivity : Activity() {
    // DataBinding
    val binding: ActivityMainBinding by databind(R.layout.activity_main)
    
    // ViewBinding
    val binding: ActivityMainBinding by viewbind()
}

class FragmentActivity : Activity() {
    // DataBinding
    val binding: ActivityMainBinding by databind(R.layout.activity_main)
    
    // ViewBinding
    val binding: ActivityMainBinding by viewbind()
}
```

* There are two ways in `Fragment`, and their use positions are different, as shown below.
    
    * Method 1: Use in `onCreateView`，[see example](https://github.com/hi-dhl/Binding/tree/main/app/src/main/java/com/hi/dhl/demo/binding/navigation)
    * Method 2: Use in `onViewCreated`，see example [ViewBindFragment.kt](https://github.com/hi-dhl/Binding/blob/main/app/src/main/java/com/hi/dhl/demo/binding/viewbind/ViewBindFragment.kt) and  [DataBindRecycleFragment.kt](https://github.com/hi-dhl/Binding/blob/main/app/src/main/java/com/hi/dhl/demo/binding/databind/list/DataBindRecycleFragment.kt)

**PS: Need to pay attention to the following points：**

* If you use Navigaion Fragment management framework, you can only use `Method 1`，[see example](https://github.com/hi-dhl/Binding/tree/main/app/src/main/java/com/hi/dhl/demo/binding/navigation) 
* Use in `BottomSheetDialogFragment` ，you can only use `Method 1`
* In other Fragment scenarios, if the ui is not displayed using `Method 2`, please use `Method 1` to solve the problem

```
Method 1：
class FragmentNav1 : Fragment(R.layout.fragment_main) {
    
    // DataBinding
  	val binding: FragmentMainBinding by databind()
    
    // ViewBinding
  	 val binding: FragmentMainBinding by viewbind()
  
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View {
        return binding.root
    }
}

Method 2：
class FragmentNav1 : Fragment(R.layout.fragment_main) {
    
    // DataBinding
  	val binding: FragmentMainBinding by databind()
    
    // ViewBinding
  	 val binding: FragmentMainBinding by viewbind()
  
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        binding.apply { textView.setText("Binding") }
    }
}
``` 

* The usage in `Dialog` is as follows。

```
class AppDialog(context: Context) : Dialog(context, R.style.AppDialog) {

    // DataBinding
    val binding: DialogAppBinding by databind(R.layout.dialog_data_binding)
    
    // ViewBinding
    val binding: DialogAppBinding by viewbind()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding.apply { result.setText("DialogAppBinding") }
    }
}
```

or add life cycle listening

```
class AppDialog(context: Context,lifecycle: Lifecycle) : Dialog(context, R.style.AppDialog) {

    // use DataBinding life cycle listening
    val binding: DialogAppBinding by databind(R.layout.dialog_data_binding, lifecycle)
    
    // use ViewBinding life cycle listening
    val binding: DialogAppBinding by viewbind(lifecycle)

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding.apply { result.setText("DialogAppBinding") }
    }
}
```

* Extension method that supports DataBinding to bind data when initialized，Thanks to `@br3ant` contribute，[see example](https://github.com/hi-dhl/Binding/blob/054aa169d8dd39023be55be589b67e8097702bd1/app/src/main/java/com/hi/dhl/demo/binding/databind/DatBindActivity.kt#L28-L33)

```
val binding: ActivityDataBindBinding by databind(R.layout.activity_data_bind) {
    val account = Account()
    account.name = "test"
    this.account = account
}
```

### proguard

```
-keepclassmembers class ** implements androidx.viewbinding.ViewBinding {
    public static ** bind(***);
    public static ** inflate(***);
}
```

### change log

**2020-12-28（V1.0.6）**

* Support Activity and Fragment to automatically bind LifecycleOwner。[see issue](https://github.com/hi-dhl/Binding/issues/8)

**2020-12-21（V1.0.5）**

* Support using DataBinding and ViewBinding in navigation fragment，[see example](https://github.com/hi-dhl/Binding/tree/main/app/src/main/java/com/hi/dhl/demo/binding/navigation)

**2020-12-17（V1.0.4）**

* Support all Adapters related to RecyclerView.ViewHolder (ListAdapter, PagingDataAdapter, RecyclerView.Adapter, etc.) to use DataBinding and ViewBinding，[see example](https://github.com/hi-dhl/Binding/blob/main/app/src/main/java/com/hi/dhl/demo/binding/databind/list/ProductAdapter.kt)

* Extension method that supports DataBinding to bind data when initialized，Thanks to `@br3ant` contribute，[see example](https://github.com/hi-dhl/Binding/blob/054aa169d8dd39023be55be589b67e8097702bd1/app/src/main/java/com/hi/dhl/demo/binding/databind/DatBindActivity.kt#L28-L33)

**2020-12-15（V1.0.3）**

* Use of DataBinding in Dialog，  `by databind(R.layout.dialog_data_binding)` or `by databind(R.layout.dialog_data_binding, lifecycle)` 
* Avoid memory leaks, have life cycle awareness, and automatically destroy data when the life cycle is in `onDestroyed()`
* The minimum SDK version is reduced to 14

**2020-12-14:**

* Demo adds DataBinding example
* Demo adds ViewBinding example
* Demo adds kotlin-parcelize example

**2020-12-13（V1.0.1）**

* Use  ViewBinding in Dialog, add `by viewbind()` or `by viewbind(lifecycle)` 

**2020-12-12（V1.0.0）**

* A simple API requires only one line of code to implement DataBinding or ViewBinding
* Support the use of DataBinding or ViewBinding in the `Activity` 、`AppCompatActivity` 、`FragmentActivity` 、`Fragment`  
* Avoid a lot of template code
* Avoid memory leaks, have life cycle awareness, and automatically destroy data when the life cycle is in `onDestroyed()`


### contact me

* 个人微信：hi-dhl
* 公众号：ByteCode，包含 Jetpack ，Kotlin ，Android 10 系列源码，译文，LeetCode / 剑指 Offer / 多线程 / 国内外大厂算法题 等等一系列文章

<img src='http://cdn.51git.cn/2020-10-20-151047.png' width = 350px/>

---

最后推荐我一直在更新维护的项目和网站：

* 计划建立一个最全、最新的 AndroidX Jetpack 相关组件的实战项目 以及 相关组件原理分析文章，正在逐渐增加 Jetpack 新成员，仓库持续更新，欢迎前去查看：[AndroidX-Jetpack-Practice](https://github.com/hi-dhl/AndroidX-Jetpack-Practice)

* LeetCode / 剑指 offer / 国内外大厂面试题 / 多线程 题解，语言 Java 和 kotlin，包含多种解法、解题思路、时间复杂度、空间复杂度分析<br/>

    <image src="http://cdn.51git.cn/2020-10-04-16017884626310.jpg" width = "500px"/>
  
    * 剑指 offer 及国内外大厂面试题解：[在线阅读](https://offer.hi-dhl.com)
    * LeetCode 系列题解：[在线阅读](https://leetcode.hi-dhl.com)

* 最新 Android 10 源码分析系列文章，了解系统源码，不仅有助于分析问题，在面试过程中，对我们也是非常有帮助的，仓库持续更新，欢迎前去查看 [Android10-Source-Analysis](https://github.com/hi-dhl/Android10-Source-Analysis)

* 整理和翻译一系列精选国外的技术文章，每篇文章都会有**译者思考**部分，对原文的更加深入的解读，仓库持续更新，欢迎前去查看 [Technical-Article-Translation](https://github.com/hi-dhl/Technical-Article-Translation)

* 「为互联网人而设计，国内国外名站导航」涵括新闻、体育、生活、娱乐、设计、产品、运营、前端开发、Android 开发等等网址，欢迎前去查看 [为互联网人而设计导航网站](https://site.51git.cn)

**感谢**

中文：

感谢 [Simple one-liner ViewBinding in Fragments and Activities with Kotlin](https://medium.com/@Zhuinden/simple-one-liner-viewbinding-in-fragments-and-activities-with-kotlin-961430c6c07c)  文章带来的思路，以及从 [Anko](https://github.com/Kotlin/anko) 、 [ViewBindingDelegate](https://github.com/hoc081098/ViewBindingDelegate) 和 jetpack 等等开源库中学习到技巧

English:

* Thanks to Google Translation
* the idea from [Simple one-liner ViewBinding in Fragments and Activities with Kotlin](https://medium.com/@Zhuinden/simple-one-liner-viewbinding-in-fragments-and-activities-with-kotlin-961430c6c07c)
* learn skills from open source libraries such as [Anko](https://github.com/Kotlin/anko) 、 [ViewBindingDelegate](https://github.com/hoc081098/ViewBindingDelegate) and jetpack


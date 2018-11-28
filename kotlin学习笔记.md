#kotlin学习笔记

###kotlin简介
  Kotlin是一门静态语言，支持多种平台，包括移动端、服务端以及浏览器端，此外，Kotlin还是一门融合了面向对象与函数式编程的语言，支持泛型、安全的空判断，并且Kotlin与Java可以做到完全的交互。
###kotlin特点
 - 代码简洁，语句结尾没有分号
 - 编译期非空判断，有效防止空指针异常
 - 支持lambda表达式
 - 完美支持java语言、java库，同一个项目可以使用java和kotlin两种语言
 - 可以使用任何java IDE或者使用命令进行构建
 
###View Binding
 > 省去了大量findViewById()操作，
 
	import kotlinx.android.synthetic.main.activity_main.*
	class MyActivity : Activity() {
	    override fun onCreate(savedInstanceState: Bundle?) {
	        super.onCreate(savedInstanceState)
	        setContentView(R.layout.activity_main)
	        
	        // Instead of findViewById<TextView>(R.id.textView)
	        textView.setText("Hello, world!")
	    }
	}
 	// textView即在xml中声明的TextView的id

###在kotlin中使用ButterKinfe
> 在 Kotlin 中使用 ButterKnife 与 Java 中完全一致。 在 Gradle 依赖中添加 kotlin-kapt 插件，并使用 kapt 替代 annotationProcessor。


	apply plugin: 'kotlin-kapt'
	​
	dependencies {
	    ...
	    compile "com.jakewharton:butterknife:$butterknife_version"
	    kapt "com.jakewharton:butterknife-compiler:$butterknife_version"
	}

> **java:**
> 在 Java 中使用注解对将变量与之对应的 view 进行绑定：


	@BindView(R2.id.title) TextView title;
> **kotlin:**在 Kotlin 中使用属性而不是直接使用变量。 对属性使用注解:


	@BindView(R2.id.title)
	lateinit var title: TextView
>@BindView 被定义为仅应用于变量字段，而将注解应用于整个属性时，Kotlin 编译器能够理解并且覆盖相应注解的字段。
lateinit 修饰符允许声明非空类型，并在对象创建后(构造函数调用后)初始化。 不使用 lateinit 则需要声明可空类型并且有额外的空安全检测操作。

使用 ButterKnife 注解可以将方法设置为监听器：


	@OnClick(R2.id.hello)
	internal fun sayHello() {
	    Toast.makeText(this, "Hello, views!", LENGTH_SHORT).show()
	}
以上代码表示点击“hello”按钮后的事件响应。 然而在 Kotlin 中使用 lambda 表达式会让代码更加简洁清晰：


	hello.setOnClickListener {
	    toast("Hello, views!")
	}
[Anko](https://github.com/Kotlin/anko)库默认提供 toast 函数。







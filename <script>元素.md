### <script>下的8个属性
  async：可选。表示应该立即开始下载脚本，但不能阻止其他页面动作，比如下载资源或等待其
他脚本加载。只对外部脚本文件有效。
  charset：可选。使用 src 属性指定的代码字符集。这个属性很少使用，因为大多数浏览器不
在乎它的值。
 crossorigin：可选。配置相关请求的CORS（跨源资源共享）设置。默认不使用CORS。crossorigin=
"anonymous"配置文件请求不必设置凭据标志。crossorigin="use-credentials"设置凭据
标志，意味着出站请求会包含凭据。
 defer：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效。
在 IE7 及更早的版本中，对行内脚本也可以指定这个属性。
 integrity：可选。允许比对接收到的资源和指定的加密签名以验证子资源完整性（SRI，
Subresource Integrity）。如果接收到的资源的签名与这个属性指定的签名不匹配，则页面会报错，
脚本不会执行。这个属性可以用于确保内容分发网络（CDN，Content Delivery Network）不会提
供恶意内容。
 language：废弃。最初用于表示代码块中的脚本语言（如"JavaScript"、"JavaScript 1.2"
或"VBScript"）。大多数浏览器都会忽略这个属性，不应该再使用它。
 src：可选。表示包含要执行的代码的外部文件。
 type：可选。代替 language，表示代码块中脚本语言的内容类型（也称 MIME 类型）。按照惯
例，这个值始终都是"text/javascript"，尽管"text/javascript"和"text/ecmascript"
都已经废弃了。JavaScript 文件的 MIME 类型通常是"application/x-javascript"，不过给
type 属性这个值有可能导致脚本被忽略。在非 IE 的浏览器中有效的其他值还有
"application/javascript"和"application/ecmascript"。如果这个值是 module，则代
码会被当成 ES6 模块，而且只有这时候代码中才能出现 import 和 export 关键字。
  
  
 HTML 4.01 为<script>元素定义了一个叫 defer 的属性。这个属性表示脚本在执行的时候不会改
变页面的结构。也就是说，脚本会被延迟到整个页面都解析完毕后再运行。因此，在<script>元素上
设置 defer 属性，相当于告诉浏览器立即下载，但延迟执行。
 #### 动态加载脚本
  除了<script>标签，还有其他方式可以加载脚本。因为 JavaScript 可以使用 DOM API，所以通过
向 DOM 中动态添加 script 元素同样可以加载指定的脚本。只要创建一个 script 元素并将其添加到
DOM 即可。
let script = document.createElement('script');
script.src = 'gibberish.js';
document.head.appendChild(script); 
  
 ### 变量
#### var 关键字
要定义变量，可以使用 var 操作符（注意 var 是一个关键字），后跟变量名（即标识符，如前所述）：
var message;
这行代码定义了一个名为 message 的变量，可以用它保存任何类型的值。ECMAScript 实现变量初始化，因
此可以同时定义变量并设置它的值。
 #### let 声明
  let 跟 var 的作用差不多，但有着非常重要的区别。最明显的区别是，let 声明的范围是块作用域，
而 var 声明的范围是函数作用域。
  1. 暂时性死区
let 与 var 的另一个重要的区别，就是 let 声明的变量不会在作用域中被提升。
  2. 全局声明
与 var 关键字不同，使用 let 在全局作用域中声明的变量不会成为 window 对象的属性（var 声
明的变量则会）。
  3. 条件声明
在使用 var 声明变量时，由于声明会被提升，JavaScript 引擎会自动将多余的声明在作用域顶部合
并为一个声明。因为 let 的作用域是块，所以不可能检查前面是否已经使用 let 声明过同名变量，同
时也就不可能在没有声明的情况下声明它。
  3.3.3 const 声明
const 的行为与 let 基本相同，唯一一个重要的区别是用它声明变量时必须同时初始化变量，且
尝试修改 const 声明的变量会导致运行时错误。
  3.3.4 声明风格及最佳实践
ECMAScript 6 增加 let 和 const 从客观上为这门语言更精确地声明作用域和语义提供了更好的支
持。行为怪异的 var 所造成的各种问题，已经让 JavaScript 社区为之苦恼了很多年。随着这两个新关键
字的出现，新的有助于提升代码质量的最佳实践也逐渐显现。
1. 不使用 var
有了 let 和 const，大多数开发者会发现自己不再需要 var 了。限制自己只使用 let 和 const
有助于提升代码质量，因为变量有了明确的作用域、声明位置，以及不变的值。
2. const 优先，let 次之
使用 const 声明可以让浏览器运行时强制保持变量不变，也可以让静态代码分析工具提前发现不
合法的赋值操作。因此，很多开发者认为应该优先使用 const 来声明变量，只在提前知道未来会有修
  改时，再使用 let。这样可以让开发者更有信心地推断某些变量的值永远不会变，同时也能迅速发现因
意外赋值导致的非预期行为。

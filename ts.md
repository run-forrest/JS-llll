### ts优点
代码的可读性和可维护性
在编译阶段就发现大部分错误，避免了很多线上bug
增强了编辑器和 IDE 的功能，包括代码补全、接口提示、跳转到定义、重构等


#### 1、基础类型
常用：boolean、number、string、array、enum、any、void
不常用：tuple、null、undefined、never

#### 2、对象类型
简单理解interface 和 type 的区别：type 更强大，interface 可以进行声明合并，type 不行；

#### 3、数组类型
项目中常见的写法，需要声明列表数据类型

#### 4、元组 tuple
元组和数组类似，但是类型注解时会不一样

赋值的类型、位置、个数需要和定义（生明）的类型、位置、个数一致。

#### 5、联合| or 交叉&类型
联合类型：某个变量可能是多个 interface 中的其中一个，用 | 分割
交叉类型：由多个类型组成，用 & 连接

#### 6、enum枚举
提高代码可维护性，统一维护某些枚举值

#### 7、泛型 T（Type）
简单说就是：泛指的类型，不确定的类型，可以理解为一个占位符（使用T只是习惯，使用任何字母都行）

#### 8、断言
断言用来手动指定一个值的类型。值 as 类型 or <类型>值

#### 9、in
在做类型保护时间，类似于数组和字符串的 includes 方法
也有遍历的作用，拿到ts类型定义的Key，获取Key还有个方法：keyof是取类型的key的联合类型 , in是遍历类型的key
#### 10、类型注解
显式的告诉代码，我们的 count 变量就是一个数字类型，这就叫做类型注解
#### 11、类型推断
如果 TS 能够自动分析变量类型， 我们就什么也不需要做了
如果 TS 无法分析变量类型的话， 我们就需要使用类型注解
#### 12、void和never
返回值类型，也算是基础类型。没有返回值的函数: void
如果一个函数是永远也执行不完的，就可以定义返回值为 never

#### 13、类型检测
1、typeof
typeof 操作符可以用来获取一个变量或对象的类型
2、instanceof
3、keyof
keyof 与 Object.keys 略有相似，只不过 keyof 取 interface 的键

用 keyof 可以更好的定义数据类型

function get<T extends object, K extends keyof T>(o: T, name: K): T[K] {
  return o[name]
}

#### 14、ts类里的关键字

public
private 类的外部不可用，继承也不行
protected 类的外部不可用，继承可以
public readOnly xxx 只读属性
static funcXXX 静态方法，不需要 new 就可以调用
abstract funcXXX 抽象类，所有子类都必须要实现 funcXXX

### 五、tsconfig
需要去了解 tsconfig.json 中一些参数的说明，具体参考官方文档tsconfig.json

1、作用：

用于标识 TypeScript 项目的根路径；
用于配置 TypeScript 编译器；
用于指定编译的文件。

2、注意事项：

tsc -init 生成 tsconfig.json，项目目录下直接 tsc,编译的时候就会走配置文件
compilerOptions 内部字段含义
项目别名配置：遇到过的一个坑，仅在项目config中配置别名不生效，需要在tsconfig.json中再配置一遍


### 六、Utility Types
Utility Types： 可以理解为基于ts封装的工具类型;

#### 1、Partial<T>
将T中所有属性转换为可选属性。返回的类型可以是T的任意子集
export interface UserModel {
  name: string;
  age?: number;
  sex: number;
}

type JUserModel = Partial<UserModel>
// =
type JUserModel = {
    name?: string | undefined;
    age?: number | undefined;
    sex?: number | undefined;
}

#### 2、Required<T>
通过将T的所有属性设置为必选属性来构造一个新的类型。与Partial相反
#### 3、Readonly<T>
将T中所有属性设置为只读
  
 #### 4、Record<K,T>
构造一个类型，该类型具有一组属性K，每个属性的类型为T。可用于将一个类型的属性映射为另一个类型。Record 后面的泛型就是对象键和值的类型。

简单理解：K对应对应的key，T对应对象的value，返回的就是一个声明好的对象
  
 #### ReturnType<T>
function T的返回类型
type T0 = ReturnType<() => string>;  // string

type T1 = ReturnType<(s: string) => void>;  // void



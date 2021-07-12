---
title: "Rust Getting Start"
date: 2021-04-29T15:17:44+08:00
draft: true
---





# 介绍

力求零开销抽象（zero-cost abstractions），把高级的特性编译成底层的代码，这样写起来很快，运行起来也很快，Rust 致力于使安全的代码也同样快速。







例如，使用大型数据结构时，适当地使用可变变量，可能比复制和返回新分配的实例更快。对于较小的数据结构，总是创建新实例，采用更偏向函数式的编程风格，可能会使代码更易理解，为可读性而牺牲性能或许是值得的。



# 3. 常见编程概念

标量（scalar）和复合（compound）



Rust 是 **静态类型**（*statically typed*）语言，也就是说在编译时就必须知道所有变量的类型。



**标量**（*scalar*）类型代表一个单独的值。Rust 有四种基本的标量类型：整型、浮点型、布尔类型和字符类型。

Rust 的 `char` 类型的大小为四个字节(four bytes)，并代表了一个 Unicode 标量值（Unicode Scalar Value），这意味着它可以比 ASCII 表示更多内容。



**复合类型**（*Compound types*）可以将多个值组合成一个类型。Rust 有两个原生的复合类型：元组（tuple）和数组（array）。









# 4. 认识所有权

第一部分由我们完成：当调用 `String::from` 时，它的实现 (*implementation*) 请求其所需的内存。这在编程语言中是非常通用的。

然而，第二部分实现起来就各有区别了。在有 **垃圾回收**（*garbage collector*，*GC*）的语言中， GC 记录并清除不再使用的内存，而我们并不需要关心它。没有 GC 的话，识别出不再使用的内存并调用代码显式释放就是我们的责任了，跟请求内存的时候一样。从历史的角度上说正确处理内存回收曾经是一个困难的编程问题。如果忘记回收了会浪费内存。如果过早回收了，将会出现无效变量。如果重复回收，这也是个 bug。我们需要精确的为一个 `allocate` 配对一个 `free`。

Rust 采取了一个不同的策略：内存在拥有它的变量离开作用域后就被自动释放。下面是示例 4-1 中作用域例子的一个使用 `String` 而不是字符串字面值的版本：











另外，这里还隐含了一个设计选择：Rust 永远也不会自动创建数据的 “深拷贝”。因此，任何 **自动** 的复制可以被认为对运行时性能影响较小。



#### [变量与数据交互的方式（一）：移动](https://kaisery.github.io/trpl-zh-cn/ch04-01-what-is-ownership.html#变量与数据交互的方式一移动)

#### [变量与数据交互的方式（二）：克隆](https://kaisery.github.io/trpl-zh-cn/ch04-01-what-is-ownership.html#变量与数据交互的方式二克隆)

#### [只在栈上的数据：拷贝](https://kaisery.github.io/trpl-zh-cn/ch04-01-what-is-ownership.html#只在栈上的数据拷贝)



Rust 不允许自身或其任何部分实现了 `Drop` trait 的类型使用 `Copy` trait。如果我们对其值离开作用域时需要特殊处理的类型使用 `Copy` 注解，将会出现一个编译时错误。







`&s1` 语法让我们创建一个 **指向** 值 `s1` 的引用



在特定作用域中的特定数据只能有一个可变引用。

我们 **也** 不能在拥有不可变引用的同时拥有可变引用。



在 Rust 中编译器确保引用永远也不会变成悬垂状态：当你拥有一些数据的引用，编译器确保数据不会在其引用之前离开作用域。

另一个没有所有权的数据类型是 *slice*。





slice 意味这一个不可变引用



# 5. 使用结构体来组织相关联的数据

注意整个实例必须是可变的；Rust 并不允许只将某个字段标记为可变。



可以使结构体存储被其他对象拥有的数据的引用，不过这么做的话需要用上 **生命周期**（*lifetimes*），这是一个第十章会讨论的 Rust 功能。生命周期确保结构体引用的数据有效性跟结构体本身保持一致。



增加注解来派生 `Debug` trait，并使用调试格式打印 `Rectangle` 实例



**方法** 与函数类似：它们使用 `fn` 关键字和名称声明，可以拥有参数和返回值，同时包含在某处调用该方法时会执行的代码。不过方法与函数是不同的，因为它们在结构体的上下文中被定义（或者是枚举或 trait 对象的上下文，将分别在第六章和第十七章讲解），并且它们第一个参数总是 `self`，它代表调用该方法的结构体实例。



:: 类型的关联函数，类似静态方法

结构体并不是创建自定义类型的唯一方法：让我们转向 Rust 的枚举功能，为你的工具箱再添一个工具。



# 6. 枚举和模式匹配

枚举是一个很多语言都有的功能，不过不同语言中其功能各不相同。Rust 的枚举与 F#、OCaml 和 Haskell 这样的函数式编程语言中的 **代数数据类型**（*algebraic data types*）最为相似。



枚举的成员类型表达了一类，面向对象的概念





# 7. 项目结构

作用域（scope）

## 包（Packages）

一个包会包含有一个 `Cargo.toml` 。

一个包中至多 **只能** 包含一个库 crate(library crate)；包中可以包含任意多个二进制 crate(binary crate)；包中至少包含一个 crate，无论是库的还是二进制的。



Cargo 遵循的一个约定：*src/main.rs* 就是一个与包同名的二进制 crate 的 crate 根。同样的，Cargo 知道如果包目录中包含 *src/lib.rs*，则包带有与其同名的库 crate，且 *src/lib.rs* 是 crate 根。crate 根文件将由 Cargo 传递给 `rustc` 来实际构建库或者二进制项目。



通过将文件放在 *src/bin* 目录下，一个包可以拥有多个二进制 crate：每个 *src/bin* 下的文件都会被编译成一个独立的二进制 crate。



### **Crates** 



## 模块（Modules）

*模块* 让我们可以将一个 crate 中的代码进行分组，以提高可读性与重用性。模块还可以控制项的 *私有性*，即项是可以被外部代码使用的（*public*），还是作为一个内部实现的内容，不能被外部代码使用（*private*）。



模块树可能会令你想起电脑上文件系统的目录树；这是一个非常恰当的比喻！就像文件系统的目录，你可以使用模块来组织你的代码。



## 路径（path）

路径有两种形式：

- **绝对路径**（*absolute path*）从 crate 根开始，以 crate 名或者字面值 `crate` 开头。
- **相对路径**（*relative path*）从当前模块开始，以 `self`、`super` 或当前模块的标识符开头。

绝对路径和相对路径都后跟一个或多个由双冒号（`::`）分割的标识符。





# 9 错误处理



### 传播错误

### 传播错误的简写：`?` 运算符







# 10 泛型、Trait和生命周期



**trait**，这是一个定义泛型行为的方法。



泛型经过编译器会确定类型



标准库中定义的 `std::cmp::PartialOrd` trait 可以实现类型的比较功能。



### [在函数定义中使用泛型](https://kaisery.github.io/trpl-zh-cn/ch10-01-syntax.html#在函数定义中使用泛型)

### [结构体定义中的泛型](https://kaisery.github.io/trpl-zh-cn/ch10-01-syntax.html#结构体定义中的泛型)

### [枚举定义中的泛型](https://kaisery.github.io/trpl-zh-cn/ch10-01-syntax.html#枚举定义中的泛型)

### [方法定义中的泛型](https://kaisery.github.io/trpl-zh-cn/ch10-01-syntax.html#方法定义中的泛型)

注意必须在 `impl` 后面声明 `T`，这样就可以在 `Point<T>` 上实现的方法中使用它了。在 `impl` 之后声明泛型 `T` ，这样 Rust 就知道 `Point` 的尖括号中的类型是泛型而不是具体类型。



好消息是：Rust 实现了泛型，使得使用泛型类型参数的代码相比使用具体类型并没有任何速度上的损失。

Rust 通过在编译时进行泛型代码的 **单态化**（*monomorphization*）来保证效率。单态化是一个通过填充编译时使用的具体类型，将通用代码转换为特定代码的过程。





*trait* 告诉 Rust 编译器某个特定类型拥有可能与其他类型共享的功能。可以通过 trait 以一种抽象的方式定义共享的行为。可以使用 *trait bounds* 指定泛型是任何拥有特定行为的类型。





但是不能为外部类型实现外部 trait。

默认实现允许调用相同 trait 中的其他方法，哪怕这些方法没有默认实现。



### [trait 作为参数](https://kaisery.github.io/trpl-zh-cn/ch10-02-traits.html#trait-作为参数)

#### [Trait Bound 语法](https://kaisery.github.io/trpl-zh-cn/ch10-02-traits.html#trait-bound-语法)

### [返回实现了 trait 的类型](https://kaisery.github.io/trpl-zh-cn/ch10-02-traits.html#返回实现了-trait-的类型)

返回一个只是指定了需要实现的 trait 的类型的能力在闭包和迭代器场景十分的有用，第十三章会介绍它们。闭包和迭代器创建只有编译器知道的类型，或者是非常非常长的类型。`impl Trait` 允许你简单的指定函数返回一个 `Iterator` 而无需写出实际的冗长的类型。









Rust 中的每一个引用都有其 **生命周期**（*lifetime*），也就是引用保持有效的作用域。

#### [借用检查器](https://kaisery.github.io/trpl-zh-cn/ch10-03-lifetime-syntax.html#借用检查器)

生命周期注解并不改变任何引用的生命周期的长短。



当从函数返回一个引用，返回值的生命周期参数需要与一个参数的生命周期参数相匹配。如果返回的引用 **没有** 指向任何一个参数，那么唯一的可能就是它指向一个函数内部创建的值，它将会是一个悬垂引用，因为它将会在函数结束时离开作用域。



综上，生命周期语法是用于将函数的多个参数与其返回值的生命周期进行关联的。一旦他们形成了某种关联，Rust 就有了足够的信息来允许内存安全的操作并阻止会产生悬垂指针亦或是违反内存安全的行为。



# 11 测试

属性（attribute）是关于 Rust 代码片段的元数据；第五章中结构体中用到的 `derive` 属性就是一个例子。



# 12 一个 I/O 项目：构建一个命令行程序



# 13 Rust 中的函数式语言功能：迭代器与闭包

Rust 的设计灵感来源于很多现存的语言和技术。其中一个显著的影响就是 **函数式编程**（*functional programming*）。函数式编程风格通常包含将函数作为参数值或其他函数的返回值、将函数赋值给变量以供之后执行等等。



Rust 的 **闭包**（*closures*）是可以保存进变量或作为参数传递给其他函数的匿名函数。

不同于函数，闭包允许捕获调用者作用域中的值。



### [闭包类型推断和注解](https://kaisery.github.io/trpl-zh-cn/ch13-01-closures.html#闭包类型推断和注解)

### [使用带有泛型和 `Fn` trait 的闭包](https://kaisery.github.io/trpl-zh-cn/ch13-01-closures.html#使用带有泛型和-fn-trait-的闭包)

可以创建一个存放闭包和调用闭包结果的结构体。该结构体只会在需要结果时执行闭包，并会缓存结果值，这样余下的代码就不必再负责保存结果并可以复用该值。你可能见过这种模式被称 *memoization* 或 *lazy evaluation* *（惰性求值）*。



`Fn` 系列 trait 由标准库提供。所有的闭包都实现了 trait `Fn`、`FnMut` 或 `FnOnce` 中的一个。





在 Rust 中，迭代器是 **惰性的**（*lazy*），这意味着在调用方法使用迭代器之前它都不会有效果。

注意 `v1_iter` 需要是可变的：在迭代器上调用 `next` 方法改变了迭代器中用来记录序列位置的状态。换句话说，代码 **消费**（consume）了，或使用了迭代器。每一个 `next` 调用都会从迭代器中消费一个项。使用 `for` 循环时无需使 `v1_iter` 可变因为 `for` 循环会获取 `v1_iter` 的所有权并在后台使 `v1_iter` 可变。

另外需要注意到从 `next` 调用中得到的值是 vector 的不可变引用。`iter` 方法生成一个不可变引用的迭代器。如果我们需要一个获取 `v1` 所有权并返回拥有所有权的迭代器，则可以调用 `into_iter` 而不是 `iter`。类似的，如果我们希望迭代可变引用，则可以调用 `iter_mut` 而不是 `iter`。



### [产生其他迭代器的方法](https://kaisery.github.io/trpl-zh-cn/ch13-02-iterators.html#产生其他迭代器的方法)



# 14 更多关于Cargo和Crates.io的内容

### [编写有用的文档注释](https://kaisery.github.io/trpl-zh-cn/ch14-02-publishing-to-crates-io.html#编写有用的文档注释)



好消息是，即使文件结构对于用户来说 **不是** 很方便，你也无需重新安排内部组织：你可以选择使用 `pub use` 重导出（re-export）项来使公有结构不同于私有结构。









# 15 智能指针

在 Rust 中，普通引用和智能指针的一个额外的区别是引用是一类只借用数据的指针；相反，在大部分情况下，智能指针 **拥有** 他们指向的数据。

智能指针通常使用结构体实现。智能指针区别于常规结构体的显著特性在于其实现了 `Deref` 和 `Drop` trait。

 `RefCell<T>` 是一个在运行时而不是在编译时执行借用规则的类型



除了数据被储存在堆上而不是栈上之外，box 没有性能损失。不过也没有很多额外的功能。它们多用于如下场景：

- 当有一个在编译时未知大小的类型，而又想要在需要确切大小的上下文中使用这个类型值的时候
- 当有大量数据并希望在确保数据不被拷贝的情况下转移所有权的时候
- 当希望拥有一个值并只关心它的类型是否实现了特定 trait 而不是其具体类型的时候  **？？？？**



通过使用 `Rc::clone` 进行引用计数，可以明显的区别深拷贝类的克隆和增加引用计数类的克隆。当查找代码中的性能问题时，只需考虑深拷贝类的克隆而无需考虑 `Rc::clone` 调用。



### [Box 允许创建递归类型](https://kaisery.github.io/trpl-zh-cn/ch15-01-box.html#box-允许创建递归类型)



`deref` 方法返回值的引用，以及 `*(y.deref())` 括号外边的普通解引用仍为必须的原因在于所有权。如果 `deref` 方法直接返回值而不是值的引用，其值（的所有权）将被移出 `self`。在这里以及大部分使用解引用运算符的情况下我们并不希望获取 `MyBox<T>` 内部值的所有权。



### [通过 `RefCell` 在运行时检查借用规则](https://kaisery.github.io/trpl-zh-cn/ch15-05-interior-mutability.html#通过-refcellt-在运行时检查借用规则)



静态分析，正如 Rust 编译器，是天生保守的。但代码的一些属性不可能通过分析代码发现：其中最著名的就是 [停机问题（Halting Problem）](https://zh.wikipedia.org/wiki/停机问题)，这超出了本书的范畴，不过如果你感兴趣的话这是一个值得研究的有趣主题。



`RefCell<T>` 正是用于当你确信代码遵守借用规则，而编译器不能理解和确定的时候。



当创建不可变和可变引用时，我们分别使用 `&` 和 `&mut` 语法。对于 `RefCell<T>` 来说，则是 `borrow` 和 `borrow_mut` 方法，这属于 `RefCell<T>` 安全 API 的一部分。



### [结合 `Rc` 和 `RefCell` 来拥有多个可变数据所有者](https://kaisery.github.io/trpl-zh-cn/ch15-05-interior-mutability.html#结合-rct-和-refcellt-来拥有多个可变数据所有者)

标准库中也有其他提供内部可变性的类型，比如 `Cell<T>`，它类似 `RefCell<T>` 但有一点除外：它并非提供内部值的引用，而是把值拷贝进和拷贝出 `Cell<T>`。还有 `Mutex<T>`，其提供线程间安全的内部可变性，我们将在第 16 章中讨论其用法。请查看标准库来获取更多细节关于这些不同类型之间的区别。



创建引用循环是一个程序上的逻辑 bug，你应该使用自动化测试、代码评审和其他软件开发最佳实践来使其最小化。













# 16 无畏并发



不幸的是，`Rc<T>` 并不能安全的在线程间共享。



几乎所有的 Rust 类型都是`Send` 的，不过有一些例外，包括 `Rc<T>`：这是不能 `Send` 的，因为如果克隆了 `Rc<T>` 的值并尝试将克隆的所有权转移到另一个线程，这两个线程都可能同时更新引用计数。

任何完全由 `Send` 的类型组成的类型也会自动被标记为 `Send`。几乎所有基本类型都是 `Send` 的，除了第十九章将会讨论的裸指针（raw pointer）。





# 19 高级特性



另一个 Rust 存在不安全一面的原因是：底层计算机硬件固有的不安全性。如果 Rust 不允许进行不安全操作，那么有些任务则根本完成不了。Rust 需要能够进行像直接与操作系统交互，甚至于编写你自己的操作系统这样的底层系统编程！



使用不安全代码的安全抽象???



不同于闭包，`fn` 是一个类型而不是一个 trait，所以直接指定 `fn` 作为参数而不是声明一个带有 `Fn` 作为 trait bound 的泛型参数。





# 20 最后的项目: 构建多线程 web server









# Reference

[我们为什么选择 Rust 实现顶尖实时通信技术](https://www.infoq.cn/article/6tyhEApHsJbHQxSOMLF1)

https://rustmagazine.github.io/

https://rustcc.cn/article?id=c45d80ee-7a54-4c7e-a67f-14bfe124f80c



[用Rust实现的各类算法](https://github.com/TheAlgorithms/Rust)



[Rust的TensorFlow](https://github.com/tensorflow/rust)

[Hackr.io投票选出的各类值得学习的Rust项目](https://hackr.io/tutorials/learn-rust)

[rustlings](https://github.com/rust-lang/rustlings)



https://doc.rust-lang.org/unstable-book/the-unstable-book.html



[分享：如何在阅读Rust项目源码中学习](https://zhuanlan.zhihu.com/p/86352307)

[Rust实现八种排序算法](https://juejin.cn/post/6844904053353218062)



[通过例子学 Rust](https://rustwiki.org/zh-CN/rust-by-example/index.html#通过例子学-rust)



# Thought

2nm cpu极限 对资源使用的极致优化是有意义的，并且没必要重复做。

rust编译时需要知道类型的占用空间，但对于递归box这种堆上的数据也无法预估，需要开发者自己评估堆上数据内存的最大值？！





关系数据库 到反范式设计 存储的映射，消息和json数据
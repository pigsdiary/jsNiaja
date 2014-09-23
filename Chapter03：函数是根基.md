本章我们将讨论：

* 为什么理解函数至关重要
* 函数是如何作为“第一类对象”存在的
* 如何调用函数
* 声明函数
* 函数的参数是如何赋值的
* 一个函数的上下文

***
你可能已经有点惊讶，当打开这本书基础部分的时候，看到要讨论的第一个主题是函数而不是对象。

我们当然会重点讨论对象（第6章），但是归结到实质问题上，像普通人一样编写javascript代码还是像忍者一样编写，最主要的区别是理解javascript是一种函数式语言。
你所编写的javascript代码的优雅程度，取决于你是否认识到这一点。

如果你正在阅读这本书，我们假定你不是新手并且已经有足够的对象基础知识（我们也将在第6章学习更高级的对象概念），但真正理解javascript函数是你可以挥舞的最重要的一个武器。
由于函数如此重要，这一章和下一章将专门用于彻底理解javascript中的函数。

值得注意的是，在javascript中，函数是第一类对象。也就是说，它们可以共存，并且可以像任何其他javascript对象一样进行处理。
就像较为普通的javascript数据类型一样，它们可以通过变量被引用，通过字面量声明，甚至可以作为函数的参数进行传递。

javascript把函数作为一等对象来处理，这从多个层面上来看都很重要，但一个明显的优势就是代码的简洁性。
先来看一段后面会再深入讨论的一段代码，在java中对一个集合进行排序操作：

    Arrays.sort(values,new Comparator<Integer>(){
        public int compare(Integer value1, Integer value2) {
            return value2 - value1;
        }
    });

下面是javascript使用函数式编写的等价代码：

    values.sort(function(value1,value2){ return value2 - value1; });

如果觉得这种写法看起来很奇怪，不用太过担心。当你读完本章，你也将成这种写法的老手，现在我们只是想让你一窥javascript作为函数式语言带来的优点之一。

本章将会深入研究javascript在函数上面的重点功能，给你打下良好的基础，让你的javascript代码可以提升到任何大师都会引以为傲的级别。

##函数的独特之处是什么

你听过多少次有人抱怨说“我讨厌javascript”？

我们愿意打赌肯定有九次十次甚至更多。造成这种现象的直接原因是，有些人试图以另一种他们熟悉的语言的方式来使用javascript。
令人沮丧的是，javascript并不是他们所想象的那样。这种事情发生在那些从其他语言转向javascript的开发者身上最为常见。
其他语言比如java，一种非函数式语言，许多开发者在投身于javascript之前都有学它。

对这些开发者来说，令事情变得更糟糕的是这门语言悲剧的命名：javascript。
暂且不去责骂语言命名背后的那段历史，如果javascript保留它原本的名字LiveScript或者给它起一个不会引起混淆的名字的话，也许开发者对它就不会有那些错误的先入为主的观念。
Because JavaScript has as much to do with Java as a hamburger has to do with ham.

Hamburgers和ham都是食物，肉类制品，就像javascript和java都是受C语言语法影响的编程语言。但除此之外，它们不具有很多共同点，从本质上来说更是不一样。

>造成开发者对javascript不太正确的认知的另一个因素是，大部分开发者都是通过浏览器接触javascript的。
>比起javascript这门语言本身，他们可能更倾向于熟悉从javascript绑定到DOM API。而DOM API……好吧，我们只能说它不会成为“年度最佳API” = =#。但是，这并不是javascript的错。

在我们学习函数在javascript中如何重要之前，我们先思考下，为什么javascript的函数式如此重要，特别是对于那些为浏览器编写的代码而言。

###为什么javascript的函数式如此重要

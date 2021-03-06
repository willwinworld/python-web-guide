.. _codingstyle:

编码之前碎碎念
=====================================================================


代码风格
--------------------------------------
不一致的开发风格会给协作开发带来困难，同时也妨碍代码阅读，读代码的时间是多于写代码的，所以有必要统一编码规范。推荐使用pep8或者其子集作为代码规范，使用vim插件python-mode开启pep8和pylint对代码就行检测。如果使用其他编辑器或者IDE工具最好也使用相关插件使代码符合规范。工程上的代码应该尽可能保持清晰易懂，推荐看看requests等优秀的开源库学习下。

* `《PEP 8 -- Style Guide for Python Code》 <https://www.python.org/dev/peps/pep-0008/>`_
* `《Google开源项目风格指南-Python风格指南》 <http://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/>`_ google风格的docstring比较赞


编程范式
--------------------------------------
Python支持多重编程范式，过程式(Procedural)，面向对象(OOP)，简单函数式(Functional)编程。不同人，不同语言转过来的人，Python老鸟和菜鸟等写出来的代码风格迥异。笔者之前的同事有对OOP挖掘较深的，一般习惯写OOP风格的，但现在的项目却很少用类，之前的代码都是用一个个函数来实现各种功能。对个人风格喜好不予评判，但是个人感觉还是需要深挖一些Python的特性，虽然Python容易入门，但是有些语言特性还是需要一段时间才能了解深入的。使用各种风格的时候要酌情判断，比如一个过程需要维护大量的中间状态时，单纯的使用函数会写得很冗长，这时候可以用类和子函数的形式简化它。当你无法判断哪种方式比较好的时候，请在解释器里边 `import this` 看看。一些参考:

* `《requests》 <https://github.com/kennethreitz/requests>`_ requests库是接口设计的典范，可以参考参考。
* `《Python3 面向对象编程》 <https://book.douban.com/subject/26468916/>`_ 关于Python面向对象和一些设计模式。
* `《OOP vs Functional Programming vs Procedural》 <http://stackoverflow.com/questions/552336/oop-vs-functional-programming-vs-procedural>`_


何谓Pythonic?
--------------------------------------
Python的世界里你会听到这个词"Pythonic"，大概就是指代码符合Python的惯用法，使用的都是Python的语法糖。比如从其他语言转到Python
的写出来的代码很可能受到以前思维方式的影响，写出来的代码不够Pythonic:
比如:


.. code-block:: python

    # 不够Pythonic
    if a < b and a > c:
        pass

    # python里却可以这么写
    if c < a < b:
        pass

    # bad
    i = 0
    while i < mylist_length:
        do_something(mylist[i])
        i += 1

    # good
    for element in mylist:
       do_something(element)

    # bad, 不要使用默认可变对象作为默认参数
    def f(a, b=[])
        pass

    # good
    def f(a, b=None):
        if b is None:
            b = []



Python有一些语法上的坑，比如默认参数只计算一次，不要使用可变类型作为默认参数等，看多了写多了就知道了。一些参考帮助写出Pythonic的代码:


* `《Pythonic到底是什么玩意儿？》 <http://blog.csdn.net/gzlaiyonghao/article/details/2762251>`_ 赖勇浩的博客
* `《python-guide Code Style》 <http://docs.python-guide.org/en/latest/writing/style/>`_ python-guide关于代码风格的介绍
* `《Learning the Pythonic Way》 <https://www.cs.cmu.edu/~srini/15-441/F11/lectures/r04-python.pdf>`_ 一个cmu的课件
* `《Writing Idiomatic Python3》 <http://share.sm3.su/writing_idiomatic_python_3.pdf>`_ 一本免费小书
* `《编写高质量代码：改善Python程序的91个建议》 <https://book.douban.com/subject/25910544/>`_ 给国人的书捧捧场^_^


敏捷与TDD
----------------------------
笔者非计算机科班出身，对于软件工程的东西也不是很懂，最近扫了一本《敏捷软件开发-原则、模式与实践》，感觉有些东西还是挺有启发的。在这里稍微提一下敏捷中的TDD(Test-driven development)吧。因为Python是动态类型语言，不像静态语言可以编译期检查，很多问题运行时暴露出来，而且动态语言语法灵活也容易刨坑。用TDD是可以提升代码质量的，虽然有时候完全用TDD可能有些死板，但是TDD的一些思想还是很值得借鉴：

* 测试最重要的是对架构和设计的影响，不是为了测试而测试。一般难以测试的代码往往是设计不好，耦合严重的代码。没有测试的代码同时也给重构带来压力和隐患。

编码的时候想着如何测试它，甚至都可以改善设计。对于动态语言，一直有『动态语言一时爽，代码重构火葬场』这种说法，说明动态语言如果没有良好的设计和测试，以后是会埋下不少隐患的。
当你发现debug的时间甚至比写代码长很多的时候，当你发现总是返工对代码修修补补的时候，或者可尝试下TDD。
你可以学习使用下python的unittest或者pytest等进行单元测试，以保证代码质量。下边是一些参考书籍:


* `《pytest: helps you write better programs》 <http://pytest.org/latest/>`_
* `《代码整洁之道》 <https://book.douban.com/subject/5442024/>`_
* `《编写可读代码的艺术》 <https://book.douban.com/subject/10797189/>`_
* `《重构-改善既有代码设计》 <https://book.douban.com/subject/4262627/>`_
* `《软件调试修炼之道》 <https://book.douban.com/subject/6398127/>`_
  了解下调试和跟踪技术。


一些常见原则
----------------------------
对于什么是好代码，什么是坏代码我现在还没有太多经验，但是最近工作接手别人的代码感觉困难重重，还是too naive啊。每个人实力不同，风格不同，一起协作的时候确实会遇到很多问题和分歧。感觉code review啥的还是很有必要的，可以让菜鸟学习下老鸟的经验，也可以让老鸟指导下菜鸟的失误，同时避免过于个人化的糟糕风格（比如让人想立马离职的高达成百上千行的复杂函数，比如上来一堆不知道干啥的幻数，比如上来就 `form shit import *` 导致俺的编辑工具找不到定义，比如整个项目没有一行测试代码，全用print+眼珠子瞅，一个bug找半天，比如没有pep8检测导致你的环境打开别人的代码彪了一堆警告......)。说好的设计模式呢，说好的高内聚低耦合呢？说好的KISS原则呢？说好的DYR原则呢？其实俺只是想多活几年，至少不要到三十岁头发掉光。啥设计模式的可以不用，能干活的代码就行，牢记几个原则，没事的时候对复杂的东西重构下，代码不能自解释的搞搞文档，不被队友坑同时不坑队友，俺就心满意足了。最后还是列举一下常用原则、思想和注意事项吧：

* KISS原则，Keep It Simple, Stupid。能简单的绝对不要复杂，不要炫耀代码技巧，简单可读最重要，后人会感谢你的。
* DRY原则。就算咱不懂设计模式，只要代码复杂重复了就及时抽取出来，至少不会碰到大问题。
* 高内聚，低耦合。写代码的时候想着怎么测试它就能避免过度复杂，耦合严重的代码。
* 代码应当易于理解。 《代码大全》、《编写可读代码的艺术》、《代码整洁之道》啥的都是告诉你代码最好自解释，好理解。记住代码首先是给人看的，其次才是让机器执行的。
* 不要过早优化。根据二八定律，大部分性能瓶颈只在20%的部分，这些才是真正需要优化的地方。
* Think about future, design with flexibility, but only implement for production. 尽量设计良好，避免繁杂和冗余。好的架构和设计都是不断演进的。
* 文档化。哪些东西该文档化，哪些该注释需要做好，以便新手可以尽快上手。尽量做到代码即文档，tornado的文档和代码就是典范。
* 不要放过任何错误和异常，一定要做好记录。血泪教训，使用Sentry或其他工具记录好异常发生的信息，为定位bug提供便利，web端的bug一般不好复现。
* ......还有的大家可以自己补充


还有OOP那一套:

* 开闭原则(Open-Closed Principle)
* 依赖倒置原则(Dependence Inversion Principle)
* 接口隔离原则(Interface Segregation Principle)
* 里氏代换原则(Liskov Substitution Principle)
* 迪米特原则(Law of Demeter)
* 合成复用原则(Composite/Aggregate Reuse Principle)
* 单一职责原则(Single-Responsibility Principle)

可能很多东西对老鸟来说都是显而易见的，不过菜鸟们还是需要多多练习积累经验。慢慢摸索吧骚年。。。。。。

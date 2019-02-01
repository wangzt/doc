# AOP 技术本质

##技术起源
AOP技术的诞生并不算晚，早在1990年开始，来自Xerox Palo Alto Research Lab（即PARC）的研究人员就对面向对象思想的局限性进行了分析。他们研究出了一种新的编程思想，借助这一思想或许可以通过减少代码重复模块从而帮助开发人员提高工作效率。随着研究的逐渐深入，AOP也逐渐发展成一套完整的程序设计思想，各种应用AOP的技术也应运而生。
AOP技术在Java平台下是最先得到应用的。就在PARC对于面向方面编程进行研究的同时，美国Northeastern University的博士生Cristina Lopes和其同事也开始了类似的思考。最终，美国国防先进技术研究计划署（Defense Advanced Research Projects Agency即DARPA）注意到了这项工作，并提供了科研经费，鼓励将二者的工作成果结合起来。他们通过定义一套Java语言的扩展系统，使开发者可以方便的进行面向方面的开发，这套扩展系统被称为AspectJ。之后，AspectJ在2002年被转让给Eclipse Foundation，从而成为在开源社区中AOP技术的先锋，也是目前最为流行的AOP工具。

##技术概览
AOP（Aspect-Oriented Programming，面向方面编程），可以说是OOP（Object-Oriented Programing，面向对象编程）的补充和完善。OOP引入封装、继承和多态性等概念来建立一种对象层次结构，用以模拟公共行为的一个集合。当我们需要为分散的对象引入公共行为的时候，OOP则显得无能为力。也就是说，OOP允许你定义从上到下的关系，但并不适合定义从左到右的关系。例如日志功能。日志代码往往水平地散布在所有对象层次中，而与它所散布到的对象的核心功能毫无关系。对于其他类型的代码，如安全性、异常处理和透明的持续性也是如此。这种散布在各处的无关的代码被称为横切（cross-cutting）代码，在OOP设计中，它导致了大量代码的重复，而不利于各个模块的重用。

而AOP技术则恰恰相反，它利用一种称为“横切”的技术，剖解开封装的对象内部，并将那些影响了多个类的公共行为封装到一个可重用模块，并将其名为“Aspect”，即方面。所谓“方面”，简单地说，就是将那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可操作性和可维护性。

使用“横切”技术，AOP把软件系统分为两个部分：**核心关注点和横切关注点**。业务处理的主要流程是核心关注点，与之关系不大的部分是横切关注点。横切关注点的一个特点是，他们经常发生在核心关注点的多处，而各处都基本相似。比如权限认证、日志、事务处理。Aop 的作用在于分离系统中的各种关注点，将核心关注点和横切关注点分离开来。正如Avanade公司的高级方案构架师Adam Magee所说，AOP的核心思想就是“**将应用程序中的商业逻辑同对其提供支持的通用服务进行分离**。”

实现AOP的技术，主要分为两大类：一是采用动态代理技术，利用截取消息的方式，对该消息进行装饰，以取代原有对象行为的执行；二是采用静态织入的方式，引入特定的语法创建“方面”，从而使得编译器可以在编译期间织入有关“方面”的代码。然而殊途同归，实现AOP的技术特性却是相同的，分别为：
1. **join point**（连接点）：是程序执行中的一个精确执行点，例如类中的一个方法。它是一个抽象的概念，在实现AOP时，并不需要去定义一个join point。
2. **point cut**（切入点）：本质上是一个捕获连接点的结构。在AOP中，可以定义一个point cut，来捕获相关方法的调用。
3. **advice**（通知）：是point cut的执行代码，是执行“方面”的具体逻辑。
4. **aspect**（方面）：point cut和advice结合起来就是aspect，它类似于OOP中定义的一个类，但它代表的更多是对象间横向的关系。
5. **introduce**（引入）：为对象引入附加的方法或属性，从而达到修改对象结构的目的。有的AOP工具又将其称为mixin。

##横切技术
“横切”是AOP的专有名词。它是一种蕴含强大力量的相对简单的设计和编程技术，尤其是用于建立松散耦合的、可扩展的企业系统时。横切技术可以使得AOP在一个给定的编程模型中穿越既定的职责部分（比如日志记录和性能优化）的操作。

如果不使用横切技术，软件开发是怎样的情形呢？在传统的程序中，由于横切行为的实现是分散的，开发人员很难对这些行为进行逻辑上的实现或更改。例如，用于日志记录的代码和主要用于其它职责的代码缠绕在一起。根据所解决的问题的复杂程度和作用域的不同，所引起的混乱可大可小。更改一个应用程序的日志记录策略可能涉及数百次编辑——即使可行，这也是个令人头疼的任务。

在AOP中，我们将这些具有公共逻辑的，与其他模块的核心逻辑纠缠在一起的行为称为“横切关注点（Crosscutting Concern）”，因为它跨越了给定编程模型中的典型职责界限。

##横切关注点
一个关注点（concern）就是一个特定的目的，一块我们感兴趣的区域，一段我们需要的逻辑行为。从技术的角度来说，一个典型的软件系统包含一些核心的关注点和系统级的关注点。举个例子来说，一个信用卡处理系统的核心关注点是借贷/存入处理，而系统级的关注点则是日志、事务完整性、授权、安全及性能问题等，许多关注点——即横切关注点（crosscutting concerns）——会在多个模块中出现。如果使用现有的编程方法，横切关注点会横越多个模块，结果是使系统难以设计、理解、实现和演进。AOP能够比上述方法更好地分离系统关注点，从而提供模块化的横切关注点。

为了建立松散耦合的、可扩展的企业系统，AOP应用到的横切技术，通常分为两种类型：**动态横切**和**静态横切**。
1. **动态横切**
动态横切是通过切入点和连接点在一个方面中创建行为的过程，连接点可以在执行时横向地应用于现有对象。动态横切通常用于帮助向对象层次中的各种方法添加日志记录或身份认证。在很多应用场景中，动态横切技术基本上代表了AOP。
动态横切技术的核心主要包括join point（连接点），point cut（切入点），advice（通知）和aspect（方面）。
2. **静态横切**
静态横切和动态横切的区别在于它不修改一个给定对象的执行行为。相反，它允许通过引入附加的方法字段和属性来修改对象的结构。此外，静态横切可以把扩展和实现附加到对象的基本结构中。在AOP实现中，通常将静态横切称为introduce或者mixin。
静态横切在AOP技术中，受到的关注相对较少。事实上，这一技术蕴含的潜力是巨大的。使用静态横切，架构师和设计者能用一种真正面向对象的方法有效地建立复杂系统的模型。静态横切允许您不用创建很深的层次结构，以一种本质上更优雅、更逼真于现实结构的方式，插入跨越整个系统的公共行为。尤其是当开发应用系统时，如果需要在不修改原有代码的前提下，引入第三方产品和API库，则静态横切技术将发挥巨大的作用。

##AOP技术的优势
AOP技术的优势是显而易见的。在面向对象的世界里，人们提出了各种方法和设计原则来保障系统的可复用性与可扩展性，以期建立一个松散耦合、便于扩展的软件系统。例如GOF提出的“设计模式”，为我们提供了设计的典范与准则。设计模式通过最大程度的利用面向对象的特性，诸如利用继承、多态，对责任进行分离、对依赖进行倒置，面向抽象，面向接口，最终设计出灵活、可扩展、可重用的类库、组件，乃至于整个系统的架构。在设计的过程中，通过各种模式体现对象的行为、暴露的接口、对象间关系、以及对象分别在不同层次中表现出来的形态。**然而鉴于对象封装的特殊性，“设计模式”的触角始终在接口与抽象中大做文章，而对于对象内部则无能为力**。

通过“横切”技术，AOP技术就能深入到对象内部翻云覆雨，截取方法之间传递的消息为我所用。由于将核心关注点与横切关注点完全隔离，使得我们能够独立的对“方面”编程。它允许开发者动态地修改静态的OO模型，构造出一个能够不断增长以满足新增需求的系统，就象现实世界中的对象会在其生命周期中不断改变自身，应用程序也可以在发展中拥有新的功能。

设计软件系统时应用AOP技术，其优势在于：
1. 在定义应用程序对某种服务（例如日志）的所有需求的时候。通过识别关注点，使得该服务能够被更好的定义，更好的被编写代码，并获得更多的功能。这种方式还能够处理在代码涉及到多个功能的时候所出现的问题，例如改变某一个功能可能会影响到其它的功能，在AOP中把这样的麻烦称之为“纠结（tangling）”。
2. 利用AOP技术对离散的方面进行的分析将有助于为开发团队指定一位精于该项工作的专家。负责这项工作的最佳人选将可以有效利用自己的相关技能和经验。
3. 持久性。标准的面向对象的项目开发中，不同的开发人员通常会为某项服务编写相同的代码，例如日志记录。随后他们会在自己的实施中分别对日志进行处理以满足不同单个对象的需求。而通过创建一段单独的代码片段，AOP提供了解决这一问题的持久简单的方案，这一方案强调了未来功能的重用性和易维护性：不需要在整个应用程序中一遍遍重新编写日志代码，AOP使得仅仅编写日志方面（logging aspect）成为可能，并且可以在这之上为整个应用程序提供新的功能。
# 代码检查


在这个页面中：

* 代码检查
    * [代码分析基础](#代码分析基础)
    * [检查配置文件](#检查配置文件)
    * [检查严重性](#检查严重性)
    * [检查区块](#检查区块)
    * [代码检查的例子](#代码检查的例子)
        * [定位无作用代码](#定位无作用代码)
        * [高亮未使用声明](#高亮未使用声明)
        * [未解决的JavaScript函数和方法](#未解决的JavaScript函数和方法)
        * [PHP代码检查例子](#PHP代码检查例子)

* [访问检查设置](/如何使用/常规指南/代码检查/访问检查设置.md)
* [分析检查结果](/如何使用/常规指南/代码检查/分析检查结果.md)
* [配置检查严重性](/如何使用/常规指南/代码检查/配置检查严重性.md)
* [改变当前文件高亮级别](/如何使用/常规指南/代码检查/改变当前文件高亮级别.md)
* [自定义配置文件](/如何使用/常规指南/代码检查/自定义配置文件.md)
* [改变区块顺序](/如何使用/常规指南/代码检查/改变区块顺序.md)
* [导出检查结果](/如何使用/常规指南/代码检查/导出检查结果.md)
* [解决问题](/如何使用/常规指南/代码检查/解决问题.md)
* [抑制检查](/如何使用/常规指南/代码检查/抑制检查.md)
* [运行检查](/如何使用/常规指南/代码检查/运行检查.md)
* [通过名称运行检查](/如何使用/常规指南/代码检查/通过名称运行检查.md)
* [离线运行检查](/如何使用/常规指南/代码检查/离线运行检查.md)
* [自动应用快速修复](/如何使用/常规指南/代码检查/自动应用快速修复.md)


## <span id='代码分析基础'>代码分析基础</span>

PhpStorm有健壮、快速、灵活的静态代码分析功能。它发现编译和运行错误，建议改正和改善在实际编译之前。

PhpStorm执行代码分析通过对代码进行检查。有大量PHP和其他支持语言的检查。

检查不仅检测编译错误，也辨别无效代码。每当你有不可访问代码，未使用代码，非限定字符串，未解析方法，内存泄漏甚至是拼写问题 - 你将极快的找到这些问题。

代码分析可以用以下几种方式执行：

* 默认的，PhpStorm分析所有打开的文件并在编辑器右侧高亮显示所有发现的代码问题。在编辑器右侧可以查看整个文件的分析状态(右上角的图标)。
    
    当发现错误，图标显示为![错误](http://image.jellychen.cn/uploads/2016/11/fail.png)；在警告的情况下为![警告](http://image.jellychen.cn/uploads/2016/11/warning.png)；如果都没问题，图标显示为![正常](http://image.jellychen.cn/uploads/2016/11/ok.png)

* 作为选择的，可以在[大部分模式](/如何使用/常规指南/代码检查/运行检查.md)下对指定的范围运行代码分析，甚至是整个项目一样大的范围。
* 如果需要，可以在指定的范围内[运行单一的代码检查](/如何使用/常规指南/代码检查/通过名称运行检查.md)

对大多数发现的问题，PhpStorm提供[快速修复建议](/如何使用/常规指南/代码检查/解决问题.md)。你可以在文件中快速审查错误通过按`F2`和`Shift+F2`在高亮行之间跳转。

更多信息和程序化描述 ，参见[配置检查严重性](/如何使用/常规指南/代码检查/配置检查严重性.md)


## <span id='检查配置文件'>检查配置文件</span>

当你检查代码，可以告诉PhpStorm你想查看那种检查类型的问题并获取相关的报告。这样配置可以储存为**检查配置文件**。

一个检查配置文件定义要查找的问题类型，例如，某些检查项的[启用/禁用](/如何使用/常规指南/代码检查/禁用和启用检查.md)状态和他们的[严重性](/如何使用/常规指南/代码检查/配置检查严重性.md)，配置文件在[检查](/参考/工具窗参考/检查工具窗.md)设置页面中配置。

要设置当前检查配置文件(在当前编辑器中用来实时代码分析），仅仅在[检查](/)设置页面中选中它并应用变更。当你[运行代码分析](/如何使用/常规指南/代码检查/运行检查.md)或[执行单一检查](/如何使用/常规指南/代码检查/通过名称运行检查.md)，可以指定对每个运行使用哪个配置文件。

<span id='基本配置文件的类型'>检查配置文件可以应用于整个IDE或指定的项目：</span>

* **项目配置文件**是可以分享的并且可以让团队成员通过VCS访问。它们储存在项目目录：`<project>/.idea/inspectionProfiles`
* **IDE配置文件**仅作为个人使用并储存在`USER_HOME/.<PhpStorm version>/config/inspection`目录的XML文件中。

PhpStorm自带以下预定义检查配置文件：

* **默认**：这个本地(IDE级别)配置文件仅作为个人使用，应用于所有项目，并储存在`USER_HOME/.<PhpStorm version>/config/inspection`目录的XML文件中。
* **项目默认**：当新的项目被创建时，项目默认配置文件从[项目模板设置](/如何使用/常规指南/配置项目和IDE设置/访问默认设置.md)中拷贝。该配置文件是可分享的并应用于当前项目。
    
    当项目创建后，任意项目默认配置文件的修改将被其他项目忽略。
    
    当[项目模板设置](/如何使用/常规指南/配置项目和IDE设置/访问默认设置.md)中的项目默认配置文件被修改了，改变的配置文件将应用于所有新创建的项目，但已存在的项目将不受影响因为它们已经有了配置文件的副本。
    
    项目默认配置文件在`<project>/.idea/inspectionProfiles`目录中储存为`Project_Default.xml`文件。
    
一个项目可以根据需要有许多检查配置文件。有两种方法创建新的配置文件：可以从项目默认配置文件的副本[添加新的配置文件](/如何使用/常规指南/代码检查/自定义配置文件.md#创建和复制配置文件)或[复制](/如何使用/常规指南/代码检查/自定义配置文件.md#创建和复制配置文件)当前选择的配置文件。新创建的配置文件储存为XML文件，位置基于[基本配置文件的类型](/#基本配置文件的类型)

每当一些对配置文件的变更被执行和接受时`<profile_name>.xml`检查配置文件中出现相应的项。该文件仅储存与默认配置文件不同的项。

更多详情参考[自定义配置文件](/如何使用/常规指南/代码检查/自定义配置文件.md)章节。


## <span id='检查严重性'>检查严重性</span>

检查严重性表示发现的代码问题对整个项目的严重性并决定在编辑器中如何高亮显示发现的问题。默认的，每个检查有以下严重性级别之一：

* **服务器问题**![服务器问题](http://image.jellychen.cn/uploads/2016/11/server_problem.png)
* **打字错误**![打字错误](http://image.jellychen.cn/uploads/2016/11/typo.png)
* **信息**![信息](http://image.jellychen.cn/uploads/2016/11/info.png)
* **弱警告**![弱警告](http://image.jellychen.cn/uploads/2016/11/weak_warning.png)
* **警告**![警告](http://image.jellychen.cn/uploads/2016/11/warning.png)
* **错误**![错误](http://image.jellychen.cn/uploads/2016/11/error.png)

可以为每个检查项增加或减少严重性级别。也就是，可以强制PhpStorm显示警告作为错误或弱警告。按相同的方法，最初的弱警告可以显示为警告或错误，或者仅作为信息。

也可以配置每个严重性级别所高亮显示的颜色和字体。除此以外，可以创建自定义严重性级别并可以对指定检查设置它们。

如果需要，可以在[不同的范围内](/如何使用/常规指南/代码检查/改变区块顺序.md)对同一个检查设置不同的严重性级别。

所有上述的检查修改将储存在[检查设置](#检查配置文件)中当前选中的[检查配置文件](/如何使用/常规指南/代码检查/访问检查设置.md)并且被应用当配置文件被使用时。


## <span id='检查区块'>检查区块</span>

默认的，所有可用的代码检查应用于所有项目文件。如果需要，可以对不同[区块](/参考/设置参数对话框/外观行为/区块.md)独立配置每个代码检查([启用/禁用](/如何使用/常规指南/代码检查/禁用和启用检查.md)，[改变它的严重性级别](/如何使用/常规指南/代码检查/配置检查严重性.md)和其他选项)。这样配置，像任意其他的检查设置 ，被保存并应用于指定[配置文件](#检查配置文件)的一部分。

可能有复杂的情况当不同区块关联配置不同的检查。当在文件中执行的检查属于一些或所有其它区块，设置为最高优先级的配置将被应用。优先级设置在[检查设置](/如何使用/常规指南/代码检查/访问检查设置.md)页面中指定位置的区块检查中配置：最顶部的配置有最高优先级。其它位置的配置的优先级较低。

更多信息和规程描述，参见[对不同范围配置检查](如何使用/常规指南/代码检查/改变区块顺序.md)


## <span id='代码检查的例子'>代码检查的例子</span>

在[检查](/参考/设置参数对话框/编辑器/检查.md)页面，所有检查项按类别分组。分析代码最常见的任务是：

* 查找可能的BUGS
* 定位无作用代码
* 检测性能问题
* 改善代码结构和可维护性
* 遵循代码指南和标准
* 遵循规范


### <span id='定位无作用代码'>定位无作用代码</span>

PhpStorm在编辑器中高亮显示无作用代码块。无作用代码是在应用程序运行期间从不会访问的代码。也许，你甚至在项目中不需要这部分代码。根据情况，这些代码可能被作为BUG或冗余。无论如何，它减少应用程序的性能并增加维护的复杂度。这有个例子。

所谓的常量条件 - 例如，条件从来不会遇见或总是为真。在这种情况下，相关的代码不可访问并且实际上是无作用代码。

![无作用代码](http://image.jellychen.cn/uploads/2016/11/code_locating.png)

PhpStorm高亮if条件如果它总是为真。所以这部分用else环绕的代码实际上是无作用代码因为它从不执行。


### <span id='高亮未使用声明'>高亮未使用声明</span>

PhpStorm也可以立即高亮显示整个项目中都不使用的Java类，方法和字段通过未使用声明检查。各种Java EE `@Inject`注释，测试代码入口点和其它隐式依赖配置，未使用声明检查相当重视这些部分。


### <span id='未解析的JavaScript函数和方法'>未解析的JavaScript函数和方法</span>

这个检查发现引用定义不明确的JavaScript函数和方法。

![未解析的JavaScript函数和方法](http://image.jellychen.cn/uploads/2016/11/js_unresolved_function_or_method.png)


### <span id='PHP代码检查例子'>PHP代码检查例子</span>

* **未解析的包含**

    这个检查发现包含不存在的文件并建议两种快速修复：用指定的名称创建文件或使用PHP文档注释。

    ![未解析的包含](http://image.jellychen.cn/uploads/2016/11/include_does_not_exist.png)


* **动态方法被作为静态调用**

    这个检查项检查是否一个静态方法调用应用于一个静态方法。

    ![动态方法被作为静态调用](http://image.jellychen.cn/uploads/2016/11/dynamic_mathod_called_as_static.png)

    `do_something()`方法被作为静态调用但实际是动态方法。


* **类中未实现的抽象方法**

    这个检查项检查是否从抽象类继承的类是否明确的声明为抽象或从超类继承的方法是否实现。

    ![类中未实现的抽象方法](http://image.jellychen.cn/uploads/2016/11/unimplemented_abstract_method_in_class.png)

    `ConcreteClass`类是从超类`AbstractClass`继承的并且没有明确的声明为抽象。与此同时，从`AbstractClass`类继承的函数`GetValue()`没有被实现。


* **参数类型**

    PHP变量没有类型，因此基本上变量类型在函数定义的时候没有指定。然而，如果一个参数明确的定义了，函数被调用时参数应该为合适的类型。

    ![参数类型](http://image.jellychen.cn/uploads/2016/11/parameter_type_inspection.png)

    函数`do_something`指定参数类型为`integer`，但调用时的参数为`string`。


* **未定义的类常量**

    这个检查项检查在类中引用的常量没有实际被定义。

    ![未定义的类常量](http://image.jellychen.cn/uploads/2016/11/undefined_constant_in_class.png)

    常量`NotExistingConst`在类`Animal`中被作为常量引用，但类中实际上没有定义。

* **未定义常量检查**

    这个检查项检查引用的常量在检查范围内没有实际被定义。

    ![未定义的常量](http://image.jellychen.cn/uploads/2016/11/undefined_constant_in_scope.png)

    被引用的常量`UndefinedConst`在检查区块中没有被定义。


* **未定义的类**

    这个检查项检查引用的类在检查范围内没有实际被定义。

    ![未定义的类](http://image.jellychen.cn/uploads/2016/11/undefined_class.png)

    被引用的类`NotExistingClass `没有被定义。


* **未定义字段**

    这个检查项检查引用的类的字段在类内没有实际被定义。

    ![未定义字段](http://image.jellychen.cn/uploads/2016/11/undefined_field.png)

    `$obj`变量是类`Animal`的一个实例。`$var`的申明包含了类`Animal`中`field`字段的引用，但是该字段没有在类中声明。

    在PHP环境中，未定义的字段和未定义的方法检查可能报告一些错误当实际上没有问题发生。这个会发生在尝试访问属性或给属性赋值，这些属性可能没有实际定义但引用的类包含get和set魔术方法。这应该不会报告错误因为这些方法每次调用或引用未定义的属性，然而，PhpStorm任然将它们作为错误或警告，基于你在检查页面设定的严重性级别。
    
    要在这种情况下抑制未定义方法的报告，[重新配置检查严重性](/如何使用/常规指南/代码检查/配置检查严重性.md)。要做到这个，打开设置对话框的[检查](/参考/设置参数对话框/编辑器/检查.md)页面，点击列表中的检查名称并在选项区域选择**Downgrade severity if \_\_magic methods are present in class**。在这之后，这种情况下未定义的属性将比通常设置显示低一级的严重性，默认的，用信息级别来代替警告级别。
    
    要抑制未定义字段不相干的报告，清空**Notify about access to a field via magic method**和**Notify about PHP dynamic field declaration**复选框。当这些复选框选中时，PhpStorm报告的错误甚至包含`__get()`和`__set()`魔术方法。


* **调用未定义的函数**

    这个检查项检查在检查范围内没有定义的函数。
    
    ![调用未定义的函数](http://image.jellychen.cn/uploads/2016/11/undefined_function_inspection.png)
    
    调用的方法`undefined_function()`没有在检测范围内定义。
    
* **未定义的变量**
    
    这个检查项检查没有在检查范围内定义和初始化的变量。PHP不需要每个变量应该被声明和初始化。PHP可以实时初始化这些变量并分配空置。然而，这个检查项可以检查到这种差异。
    
    未定义的变量检查可以在设置对话框的检查页面中通过勾选复选框来配置。    
    
    * **在全局空间中检查**：选择复选框来运行检查不在函数方法，类和命名空间中的变量，也就是[全局空间](http://php.net/manual/en/language.namespaces.global.php)
    
        ![在全局空间中检查](http://image.jellychen.cn/uploads/2016/11/ps_undefined_var_global_space_on.png)
        
    * **报告可能没有定义的变量**：选择复选框来显示警告即使变量的定义没有明确的缺失。这种情况可能发生当这个变量在多个路径中使用并且一些地方不能到达，例如，`if()`语句：
    
        ![报告可能没有定义的变量](http://image.jellychen.cn/uploads/2016/11/ps_undefined_var_if_statement.png)
        
    * **忽略'include'和'require'语句**：抑制检查包含`include**和**require`语句的范围。如果复选框没有勾选，PhpStorm处理这种定义在类中的变量并通过这种语句引用的不会报告错误。如果复选框被选中，未定义的变量错误将报告。
        
        ![忽略'include'和'require'语句](http://image.jellychen.cn/uploads/2016/11/undefined_variable_inspection.png)



# 另请参阅：

规程：

* [意向动作](/如何使用/常规指南/意向动作/README.md)

参考：

* [检查](/参考/设置参数对话框/编辑器/检查.md)
* [区块](/参考/设置参数对话框/外观行为/区块.md)
* [检查工具窗](/参考/工具窗参考/检查工具窗.md)
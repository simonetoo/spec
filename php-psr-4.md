## Autoloader

### 1. 概述
本规范是关于由文件路径 [自动加载](http://php.net/autoload) 对应类的相关规范，
本规范是可互操作的，可以作为任一自动载入规范的补充，
本规范还包括自动载入的类对应的文件存放路径规范。

###  2. 详细说明
1.此处的“类”泛指所有的class类、接口、traits可复用代码块以及其它类似结构。
2.一个完整的类名需具有以下结构:
    `\<命名空间>(\<子命名空间>)*\<类名>`
    - 完整的类名必须要有一个顶级命名空间，被称为 "vendor namespace"；
    - 完整的类名可以有一个或多个子命名空间；
    - 完整的类名必须有一个最终的类名；
    - 完整的类名中任意一部分中的下滑线都是没有特殊含义的；
    - 完整的类名可以由任意大小写字母组成；
    - 所有类名都必须是大小写敏感的。
3. 当根据完整的类名载入相应的文件……
    - 完整的类名中，去掉最前面的命名空间分隔符，前面连续的一个或多个命名空间和子命名空间，作为“命名空间前缀”，其必须与至少一个“文件基目录”相对应；
    - 紧接命名空间前缀后的子命名空间必须与相应的”文件基目录“相匹配，其中的命名空间分隔符将作为目录分隔符。
    - 末尾的类名必须与对应的以 .php 为后缀的文件同名。
    - 自动加载器（autoloader）的实现一定不能抛出异常、一定不能触发任一级别的错误信息以及不应该有返回值。
### 3. 例子
下表展示了符合规范完整类名、命名空间前缀和文件基目录所对应的文件路径。

完整类名	命名空间前缀	文件基目录	文件路径
\Acme\Log\Writer\File_Writer	Acme\Log\Writer	./acme-log-writer/lib/	./acme-log-writer/lib/File_Writer.php
\Aura\Web\Response\Status	Aura\Web	/path/to/aura-web/src/	/path/to/aura-web/src/Response/Status.php
\Symfony\Core\Request	Symfony\Core	./vendor/Symfony/Core/	./vendor/Symfony/Core/Request.php
\Zend\Acl	Zend	/usr/includes/Zend/	/usr/includes/Zend/Acl.php
关于本规范的实现，可参阅 相关实例
注意：实例并不属于规范的一部分，且随时会有所变动。
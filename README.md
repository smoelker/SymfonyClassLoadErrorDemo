## Problem
I'm trying to setup a custom directory structure 
for some shared classes in my Symfony project. I
want to create a custom folder in the root of my
project and I want to use the Symfony auto-load 
feature to automatically register services from 
that folder.

So I added a custom services namespace to the
services.yaml file:

```yaml
# src ./config/services.yaml
services:
  ...

    TestNamespace\:
      resource: '../TestNamespace/*'
      
  ...
```

And I added an empty class in the custom folder:

```php
<?php
# src ./TestNamespace/TestClass.php

namespace TestNamespace;

class TestClass
{

}
```

When I run the app I get the following error:

```
(1/2) InvalidArgumentException
Expected to find class "TestNamespace\TestClass" in file 
"/path/to/ClassLoadErrorDemo/demo/TestNamespace/TestClass.php"
while importing services from resource 
"../TestNamespace/*", but it was not found! Check the
namespace prefix used with the resource.


(2/2) FileLoaderLoadException
Expected to find class "TestNamespace\TestClass" in file 
"/path/to/ClassLoadErrorDemo/demo/TestNamespace/TestClass.php" 
while importing services from resource 
"../TestNamespace/*", but it was not found! Check the
namespace prefix used with the resource in 
/path/to/ClassLoadErrorDemo/demo/config/services.yaml 
(which is loaded in resource 
"/path/to/ClassLoadErrorDemo/demo/config/services.yaml").
```


I double checked the paths, namespace and the class 
name multiple times and everything seems fine and I 
don't understand why I still get the error.

##Steps to reproduce

I created a demo repo to isolate the problem.

```
git clone https://github.com/smoelker/SymfonyClassLoadErrorDemo.git
cd SymfonyClassLoadErrorDemo/demo
composer install
mv TestNamespace/TestClass.php_ TestNamespace/TestClass.php
php bin/console server:start
```

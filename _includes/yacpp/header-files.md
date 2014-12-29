# Header Files

In general, every **.cpp** file should have an associated **.hpp** file. There are some common exceptions such as **.cpp** files containing just a _main()_ function.

## Include guards

All header files should have an include guard to prevent multiple inclusions. The format of the symbol name should be \_\_$PROJECT\_NAME\_[$PATH]\_$FILE\_NAME\_HPP\_\_.

To guarantee uniqueness, they should be based on the full path in a project's source tree. For example, the file _foo/src/bar/baz.hpp_ in project foo should have the following guard:

{% highlight cpp %}
#ifndef __FOO_BAR_BAZ_HPP__
#define __FOO_BAR_BAZ_HPP__

// ...

#endif
{% endhighlight %}

**Not recommended but**: If you can ensure that each file name is unique you can also strip the path from the symbol name:

{% highlight cpp %}
#ifndef __FOO_BAZ_HPP__
#define __FOO_BAZ_HPP__

// ...

#endif
{% endhighlight %}

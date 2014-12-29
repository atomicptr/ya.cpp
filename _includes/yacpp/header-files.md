# Header Files

In general, every **.cpp** file should have an associated **.hpp** file. There are some common exceptions such as **.cpp** files containing just a _main()_ function.

## Include guards

All header files should have an include guard to prevent multiple inclusions. The format of the symbol name should be \_\_$PROJNAME\_$PATH\_$FILENAME\_HPP\_\_.

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

## Order of Includes

You should group and order your includes like this:

1. Standard libs like: algorithm, map or vector
2. Other 3rd party libs like: boost or SDL2
3. Project specific includes: my\_project/include/my\_project/foobar.hpp

**Hint:** Try to order them alphabetically in their groups

**For example:**

{% highlight cpp %}
#include <algorithm>
#include <string>
#include <vector>

#include <boost/filesystem.hpp>
#include <SDL2/SDL.h>

#include <my_project/foobar.hpp>

// ...
{% endhighlight %}

## Namespaces

You should always have a namespace with your project name.

**For instance:**

{% highlight cpp %}
namespace my_project {
    // ...
}
{% endhighlight %}

Having nested namespaces is encouraged as long as you don't nest them too much.

{% highlight cpp %}
namespace my_engine {
    namespace input {
        // ...
    }
}
{% endhighlight %}

### Using namespace

You are **not** allowed to use ``using namespace ...;`` in a header file. Using ``using namespace`` in a header file is bad practice as it can unexpectedly change the meaning of code in any other files that include that header. There's no way to undo a ``using namespace`` which is another reason it's so dangerous.

## Prefer C++ standard libraries

You should prefer C++ standard libraries and try not to use the old C libs. For instance prefer using **\<string\>** instead of **\<cstring\>**

If you need to use a C standard library for some reason prefer the C++ includes e.g. **\<cmath\>** to **\<math.h\>**.

**Examples:**

{% highlight cpp %}
#include <cassert> // instead of assert.h
#include <cctype> // instead of ctype.h
#include <cerrno> // instead of errno.h
#include <cfloat> // instead of float.h
#include <ciso646> // instead of iso646.h
#include <climits> // instead of limits.h
#include <clocale> // instead of locale.h
#include <cmath> // instead of math.h
#include <csetjmp> // instead of setjmp.h
#include <csignal> // instead of signal.h
#include <cstdarg> // instead of stdarg.h
#include <cstdbool> // instead of stdbool.h
#include <cstddef> // instead of stddef.h
#include <cstdint> // instead of stdint.h
#include <cstdio> // instead of stdio.h
#include <cstdlib> // instead of stdlib.h
#include <cstring> // instead of string.h
#include <ctime> // instead of time.h
#include <cuchar> // instead of uchar.h
#include <cwchar> // instead of wchar.h
#include <cwctype> // instead of wctype.h
{% endhighlight %}

## Nonmember, Static member and Global functions

Prefer Nonmember and static member functions to global functions and **always** put them into a namespace to avoid the pollution of the global namespace.

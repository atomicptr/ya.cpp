# Classes

## Creating objects

A constructor should always return a valid object.

{% highlight cpp %}
my_type t{2, 3};
{% endhighlight %}

**Avoid** two-step initialization, because it can leave your object in a half initialized state:

{% highlight cpp %}
my_type t{2, 3};

t.init(); // Bad practice!
{% endhighlight %}

**IF** you really need to do two-step initialization prefer writing a static factory method and make the initialization method and the constructor private:

{% highlight cpp %}
class my_type {
public:
    // ...

    static auto create(int x, int y) {
        my_type t{x, y};

        t.init();

        return t;
    }
private:
    // ...
    my_type(int, int);
    void init();
}
{% endhighlight %}

Usage:

{% highlight cpp %}
auto t = my_type::create(2, 3);
{% endhighlight %}

## Initialization

If your class contains member variables, you **must** provide an in-class initializer for every member variable or write a constructor (which can be a default constructor). If you do not declare any constructors yourself then the compiler will generate a default constructor for you, which may leave some fields uninitialized or initialized to inappropriate values.

## Explicit constructors

Make one-argument constructors ``explicit``.

Normally, if a constructor can be called with one argument, it can be used as a conversion. For instance, if you define ``my_type::my_type(std::string name)`` and then pass a string to a function that expects a ``my_type``, the constructor will be called to convert the string into a ``my_type`` and will pass the ``my_type`` to your function for you. This can be convenient but is also a source of trouble when things get converted and new objects created without you meaning them to. Declaring a constructor explicit prevents it from being invoked implicitly as a conversion.

In addition to single-parameter constructors, this also applies to constructors where every parameter after the first has a default value, e.g., ``my_type::my_type(std::string name, int id = 42)``.

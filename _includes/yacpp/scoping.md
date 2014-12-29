# Scoping

## Local variables

Place a function's variables in the narrowest scope possible, and initialize variables in the declaration.

C++ allows you to declare variables anywhere in a function. We encourage you to declare them in as local a scope as possible, and as close to the first use as possible. This makes it easier for the reader to find the declaration and see what type the variable is and what it was initialized to. In particular, initialization should be used instead of declaration and assignment, e.g.:

**Do:**

{% highlight cpp %}
int x = f(); // Good -- declaration has initialization

std::vector<int> v{1, 2}; // Good -- v starts initialized.
{% endhighlight %}

**Don't:**

{% highlight cpp %}
int x;
x = f(); // Bad -- initialization separate from declaration.

std::vector<int> v;
v.push_back(1); // Prefer initializing using brace initialization.
v.push_back(2);
{% endhighlight %}

Variables needed for if, while and for statements should normally be declared within those statements, so that such variables are confined to those scopes. E.g.:

{% highlight cpp %}
while(auto x = get_next_thing()) {
    x.do_something();
}
{% endhighlight %}

There is one caveat: if the variable is an object, its constructor is invoked every time it enters scope and is created, and its destructor is invoked every time it goes out of scope.

{% highlight cpp %}
for(auto i = 0u; i < 1000000; i++) {
    proj::foo f;
    f.do_something(i);
}
{% endhighlight %}

It may be more efficient to declare such a variable used in a loop outside that loop:

{% highlight cpp %}
proj::foo f;

for(auto i = 0u; i < 1000000; i++) {
    f.do_something(i);
}
{% endhighlight %}

## Static and global variables

Static or global variables of class type are forbidden: they cause hard-to-find bugs due to indeterminate order of construction and destruction. However, such variables are allowed if they are ``constexpr``: they have no dynamic initialization or destruction.

Global variables of non-class types should always be in a namespace.

## Local static variables

Always prefer local static variables to redundant member variables.

For instance:

{% highlight cpp %}
int next() {
    static auto i = 0u;

    return i++;
}
{% endhighlight %}

We don't need ``i`` as a member but we need to store the value. Local static variables are the right tool for such cases.

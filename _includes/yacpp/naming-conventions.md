# Naming

## General Naming Rules

Function names, variable names, and filenames should be descriptive; avoid abbreviation.

Names should be as descriptive as possible, within reason. Don't worry about horizontal space as it's far more important to make your code immediately understandable. Do not use abbrevations that are ambiguous or unfamiliar to readers which are not involved in the project. DO NOT ABBREVIATE BY DELETING LETTERS WITHIN A WORD.

**Do:**

{% highlight cpp %}
auto number_of_lines = 1337; // No abbreviation
auto num_items = 5; // "num" is a widely known abbrevation
{% endhighlight %}

**Don't:**

{% highlight cpp %}
int n; // meaningless
int nerr; // ambiguous abbreviation
int n_comp_conns; // ambiguous abbreviation
int gs_manager; // only your team knows what this stands for
int pc_counter; // "pc" could mean a lot of things
int cstmr_id; // deletes internal letters
{% endhighlight %}

## File Names

Filenames should be all lowercase and can include underscores (\_).

**Examples of acceptable file names:**

* main.cpp
* entity.cpp
* entity.hpp
* input_system.cpp
* input_system.hpp

C++ files should end in **.cpp** and header files should end in **.hpp**.

Do not use filenames that already exist in /usr/include

In general make your filenames very specific. For instance, use http\_server\_logs.hpp rather then logs.hpp. A very common case is to have a pair of tiles called, e.g., entity\_manager.hpp and entitiy\_manager.cpp, defining a class called entitiy\_manager.

## Type Names

Type names should be all lowercase with underscores (\_) between each new word: entity\_manager, http\_client.

The names of all types - classes, structs and enums - have the same naming conventions.

**For example:**

{% highlight cpp %}
// classes and structs
class url_table { /* .. */ };
class url_table_tester { /* ... */ }
struct url_table_properties { /* ... */ }

// enums
enum class url_table_errors { /* ... */ }
{% endhighlight %}

## Variable Names

The names of variables and data members are all lowercase, with underscores between words. Member variables of classes (but not structs) also have trailing underscores. For instance: position\_, owner\_, table\_of\_contents\_.

### Common Variable names

**For example:**

{% highlight cpp %}
std::string table_name; // OK - uses underscore
std::string tablename; // OK - all lowercase
std::String tableName; // BAD - mixed case
{% endhighlight %}

### Class Member Variables

Member variables of classes, both static and non-static, are named like ordinary nonmember variables, but with a trailing underscore.

{% highlight cpp %}
class table_info {
private:
    std::string table_name_; // OK - underscore at the end
    std::string tablename_; // OK.
    static pool<table_info>* pool_; // OK.
};
{% endhighlight %}

### Struct Member Variables

Member variables of structs, both static and non-static are named like ordinary nonmember variables. They don't have the trailing underscores that member variables in classes have.

{% highlight cpp %}
struct url_table_properties {
    std::string name;
    int num_entries;
    static pool<url_table_properties>* pool;
};
{% endhighlight %}



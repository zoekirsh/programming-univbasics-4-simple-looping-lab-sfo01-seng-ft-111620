# Simple Loops Lab

## Learning Goals

- Use loops in combination with methods
- Use loops to work with arrays

## Introduction

Loops can be potent tools in combination with methods. In this lab, we are
going to explore using loops and methods in conjunction.

## Instructions

Your task is to write four methods, `loop_message_five_times`,
`loop_message_n_times`, `output_array`, and `return_string_array`. Each method
uses a loop in a slightly different way:

### `loop_message_five_times`

The `loop_message_five_times` method has one parameter - a message string. Write
this method so that the string parameter is output five times with `puts`.

### `loop_message_n_times`

The `loop_message_n_times` method is similar to the previous method. However,
this method should take in _two_ parameters, a message string and an integer.
Write this method so that the number of times the message is output is equal
to the provided integer.

### `output_array`

The `output_array` method takes one parameter, an array. This method should
loop over the array and output each element using `puts`. For instance, if I
had the following array:

```rb
2.6.1 :001 > quote = ["All great achievements", "require time", "- Maya Angelou"]
 => ["All great achievements", "require time", "- Maya Angelou"]
```

And I passed it into `output_array`, I should get the following:

```sh
2.6.1 :002 > output_array(quote)
All great achievements
require time
- Maya Angelou
 => nil
```

### `return_string_array`

The `return_string_array` method also takes one parameter, an array. This time
is slightly different - instead of outputting anything, this method should
_return_ an array. This method should loop over the provided array, convert each
element to a string, and return the new array of strings.

Use `learn` to see your progress as you go, and `learn submit` once you've
passed all the tests. Try your best to solve these. Below is a walkthrough in
case you get stuck.

..

## Solving this Lab

This lab involves four variations on the same method structure - a loop inside a
method that uses method parameters:

```rb
def method_name(parameter)
  count = 0
  while count < (something)
    # do something with the parameter
    count += 1
  end
end
```

The first one, the `loop_message_five_times` method, uses a hard-coded loop to output the parameter:

```rb
def loop_message_five_times(message)
  count = 0
  while count < 5 do
    puts message
    count += 1
  end
end
```

A handy method if you ever need to output something five times. The second
method, `loop_message_n_times`, gives us a bit more flexibility by allowing us
to customize the number of loops the code should perform. We do this by
replacing the hard-coded `5` with the second parameter:

```rb
def loop_message_n_times(message, limit)
  count = 0
  while count < limit do
    puts message
    count += 1
  end
end
```

Now we have a slightly more versatile method. Loop messages however many times
you would like! Instead of looping the same output over any over, it would be nice
to mix it up a little. With an array, we can store a whole set of strings and
use a loop to output them all. In `output_array` this can be achieved with
the following:

```rb
def output_array(array)
  count = 0
  while count < array.length do
    puts array[count]
    count += 1
  end
end
```

No matter the length of the array provided, this code will always loop over
every element.

The final method, `return_string_array`, also loops over an array. This
time, it converts each element in the array to a string. This method needs to
_return_ an array of these converted values.

We know we will need to create a loop that will run through each element of the
array.

```rb
def return_string_array(array)
  count = 0
  while count < array.length do

    count += 1
  end
end
```

`Integer`s, `Date`s, and even `Array`s can be converted to strings using the
`.to_s` method that is built in to each class. Regardless of what is included in
the provided array, we can loop through and convert everything with the `.to_s`
command:

```rb
def return_string_array(array)
  count = 0
  while count < array.length do
    array[count].to_s
    count += 1
  end
end
```

The above code covers the conversion, but we still need to return these values. The
solution is to create a new, empty array before the loop. During every loop, we
store the newly converted string value in the new array. At the end of the
method, we return this new array:

```rb
def return_string_array(array)
  count = 0
  new_array = []
  while count < array.length do
    new_array.push(array[count].to_s) # OR new_array << array[count].to_s
    count += 1
  end
  new_array
end
```

This method should now return a new array full of the string versions of the
original array.

**Note:** One important thing to keep in mind - there is an alternative solution
some of you may have discovered. Instead of creating a new array, we _could_
modify the passed in array, replacing each element with its string version. This
solution would look like the following:

```rb
def return_string_array(array)
  count = 0
  while count < array.length do
    array[count] = array[count].to_s
    count += 1
  end
  array
end
```

The tests will not fault you for this. However, there is an important "gotcha"
early programmers fall for that should be recognized here. In the previous
solution, we created and returned a _new_ array. Whatever the original array
was, it remained unaltered. If you passed the following array into
`return_string_array`:

```sh
2.6.1 :001 > original_array = [1, 2, 3]
 => [1, 2, 3]
2.6.1 :002 > return_string_array(original_array)
 => ["1", "2", "3"]
```

...the `original_array` is unchanged:

```sh
2.6.1 :003 > original_array
 => [1, 2, 3]
```

The `original_array` variable is still integers. In this alternative solution,
the original array **gets altered:**

```sh
2.6.1 :001 > original_array = [1, 2, 3]
 => [1, 2, 3]
2.6.1 :002 > return_string_array(original_array)
 => ["1", "2", "3"]
2.6.1 :003 > original_array
 => ["1", "2", "3"]
```

One reason we prefer to create a new array - in a more extensive application, many
methods might use the original array and changing it could have unexpected
consequences. There might be use cases for this, but for the purpose of this
method, we are just deriving string values from the original array; we do not
need to modify the original array, so it is better to leave it alone.

## Conclusion

The combination of a method and a loop can be used to work through arrays,
making them very useful. These sorts of tasks are so common that there are
built-in ways to do these tasks called [Enumerables][], which we will learn
about shortly. When you get there, though, know that there is no magic in them -
you can create them all with simple loops and have done so already!

[Enumerables]: https://ruby-doc.org/core-2.7.0/Enumerable.html

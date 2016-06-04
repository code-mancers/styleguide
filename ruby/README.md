# Ruby Style Guide

Thanks to Airbnb, Github and bbatsov for giving us a great starting point.

## Table of Contents
  1. [Whitespace](#whitespace)
    1. [Indentation](#indentation)
    1. [Inline](#inline)
    1. [Newlines](#newlines)
  1. [Line Length](#line-length)
  1. [Commenting](#commenting)
    1. [File/class-level comments](#fileclass-level-comments)
    1. [Function comments](#function-comments)
    1. [Block and inline comments](#block-and-inline-comments)
    1. [Punctuation, spelling, and grammar](#punctuation-spelling-and-grammar)
    1. [TODO comments](#todo-comments)
    1. [Commented-out code](#commented-out-code)
  1. [Methods](#methods)
    1. [Method definitions](#method-definitions)
    1. [Method calls](#method-calls)
  1. [Conditional Expressions](#conditional-expressions)
    1. [Conditional keywords](#conditional-keywords)
    1. [Ternary operator](#ternary-operator)
  1. [Syntax](#syntax)
  1. [Naming](#naming)
  1. [Classes](#classes)
  1. [Exceptions](#exceptions)
  1. [Collections](#collections)

## Whitespace

### Indentation

* <a name="default-indentation"></a>Use soft-tabs with a two
    space-indent.<sup>[[link](#default-indentation)]</sup>

* <a name="indent-when-as-case"></a>Indent `when` as deep as `case`.
    <sup>[[link](#indent-when-as-case)]</sup>

    ```ruby
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end

    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end
    ```

* <a name="indent-multi-line-bool-chain"></a>Indent succeeding lines in multi-line
    boolean or chainedexpressions.<sup>[[link](#indent-multi-line-bool-chain)]</sup>

    ```ruby
    # bad
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
      is_in_program?(user) &&
      program_not_expired
    end

    # good
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
        is_in_program?(user) &&
        program_not_expired
    end
    ```

    ```ruby
    # bad
    params.
    require(:user).
    permit(:first_name, :last_name)

    # good
    params.
      require(:user).
      permit(:first_name, :last_name)
    ```

### Inline

* <a name="trailing-whitespace"></a>Never leave trailing whitespace.
    <sup>[[link](#trailing-whitespace)]</sup>

* <a name="space-before-comments"></a>When making inline comments, include a
    space between the end of the code and the start of your comment.
    <sup>[[link](#space-before-comments)]</sup>

    ```ruby
    # bad
    result = func(a, b)# we might want to change b to c

    # good
    result = func(a, b) # we might want to change b to c
    ```

* <a name="spaces-operators"></a>Use spaces around operators; after commas,
    colons, fullstops and semicolons; and around `{` and before `}`.
    <sup>[[link](#spaces-operators)]</sup>

    ```ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    ```

* <a name="spaces-block-braces"></a>In blocks, use spaces around `{` and before `}`.
    <sup>[[link](#spaces-block-braces)]</sup>

    ```ruby
    [1, 2, 3].each { |e| puts e }
    ```

* <a name="spaces-hash-braces"></a>In hashes, do not use spaces after `{` and
    before `}`. <sup>[[link](#spaces-hash-braces)]</sup>

    ```ruby
    hash = {key1: value1, key2: value2}
    ```

* <a name="no-space-before-commas"></a>Never include a space before a comma.
    <sup>[[link](#no-space-before-commas)]</sup>

    ```ruby
    result = func(a, b)
    ```

* <a name="spaces-block-params"></a>Do not include space inside block
    parameter pipes. Include one space between parameters in a block.
    Include one space outside block parameter pipes.
    <sup>[[link](#spaces-block-params")]</sup>

    ```ruby
    # bad
    {}.each { | x,  y |puts x }

    # good
    {}.each { |x, y| puts x }
    ```

* <a name="no-space-after-!"></a>Do not leave space between `!` and its
    argument.<sup>[[link](#no-space-after-!)]</sup>

    ```ruby
    !something
    ```

* <a name="no-spaces-braces"></a>No spaces after `(`, `[` or before `]`, `)`.
    <sup>[[link](#no-spaces-braces)]</sup>

    ```ruby
    some(arg).other
    [1, 2, 3].length
    ```

* <a name="no-spaces-string-interpolation"></a>Omit whitespace when doing
    string interpolation.<sup>[[link](#no-spaces-string-interpolation)]</sup>

    ```ruby
    # bad
    var = "This #{ foobar } is interpolated."

    # good
    var = "This #{foobar} is interpolated."
    ```

* <a name="no-spaces-range-literals"></a>Don't use extra whitespace in range
    literals.<sup>[[link](#no-spaces-range-literals)]</sup>

    ```ruby
    # bad
    (0 ... coll).each do |item|

    # good
    (0...coll).each do |item|
    ```

### Newlines

* <a name="newline-different-indent"></a>Don’t include newlines between areas
    of different indentation (such as around class or module bodies).
    <sup>[[link](#newline-different-indent)]</sup>

    ```ruby
    # bad
    class Foo

      def bar
        # body omitted
      end

    end

    # good
    class Foo
      def bar
        # body omitted
      end
    end
    ```

* <a name="newline-between-methods"></a>Include exactly one new
    line between methods.<sup>[[link](#newline-between-methods)]</sup>

    ```ruby
    def a
    end

    def b
    end
    ```

* <a name="method-def-empty-lines"></a>Use a single empty line to break between
    statements to break up methods into logical paragraphs internally.
    <sup>[[link](#method-def-empty-lines)]</sup>

    ```ruby
    def transformorize_car
      car = manufacture(options)
      t = transformer(robot, disguise)

      car.after_market_mod!
      t.transform(car)
      car.assign_cool_name!

      fleet.add(car)
      car
    end
    ```

* <a name="trailing-newline"></a>End each file with exactly one newline after the last
*   character of the file.
    <sup>[[link](#trailing-newline)]</sup>

## Line Length

* Keep each line of code to a readable length. Unless
  you have a reason to, keep lines to fewer than 100 characters.
  <sup> [[link](#line-length)]</sup>

## Commenting

### TODO comments

Use TODO comments for code that is temporary, a short-term solution, or
good-enough but not perfect.

TODOs should include the string TODO in all caps, followed by one colon,
followed by the full name of the person who can best provide context about the
problem referenced by the TODO, in parentheses.A comment explaining what there is
to do is required.
A TODO is not a commitment that the person referenced will fix the problem.
When you create a TODO, it is almost always your name that is given.

```ruby
  # bad - do not use nicknames or short forms of names
  # TODO: (RS) Use proper namespacing for this constant.

  # bad - do not use github or other handles even if commonly known
  # TODO: (drumm3rz4lyfe) Use proper namespacing for this constant.

  # good - use full name
  # TODO: (Ringo Starr) Use proper namespacing for this constant.
```

### Commented-out code

* <a name="commented-code"></a>Never leave commented-out code in our codebase.
    Don't be afraid to remove code even if you suspect you may need it later.
    Version control exists for that reason.
    <sup>[[link](#commented-code)]</sup>

## Methods

### Method definitions

* <a name="method-def-parens"></a>Use `def` with parentheses when there are
    parameters. Omit the parentheses when the method doesn't accept any
    parameters.<sup>[[link](#method-def-parens)]</sup>

     ```ruby
     def some_method
       # body omitted
     end

     def some_method_with_parameters(arg1, arg2)
       # body omitted
     end
     ```

### Method calls

* <a name="space-method-call"></a>Never put a space between a method name and
    the opening parenthesis.<sup>[[link](#space-method-call)]</sup>

    ```ruby
    # bad
    f (3 + 2) + 1

    # good
    f(3 + 2) + 1
    ```

* <a name="no-args-parens"></a>**Omit parentheses** for a method call if the
    method accepts no arguments.<sup>[[link](#no-args-parens)]</sup>

    ```ruby
    # bad
    nil?()

    # good
    nil?
    ```

* <a name="no-return-parens"></a>If the method doesn't return a value (or we
    don't care about the return), parentheses are optional. (If the
    arguments overflow to multiple lines, parentheses may add readability.)
    <sup>[[link](#no-return-parens)]</sup>

    ```ruby
    # okay
    render(partial: 'foo')

    # okay
    render partial: 'foo'
    ```

## Conditional Expressions

### Conditional keywords

* <a name="no-and-or"></a>The `and`, `or`, and `not` keywords are banned. It's
    just not worth it. Always use `&&`, `||`, and `!` instead.
    <sup>[[link](#no-and-or)]</sup>

* <a name="only-simple-if-unless"></a>Modifier `if/unless` usage is okay when
    the body is simple, the condition is simple, and the whole thing fits on
    one line. Otherwise, avoid modifier `if/unless`.
    <sup>[[link](#only-simple-if-unless)]</sup>

    ```ruby
    # bad - this doesn't fit on one line
    add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[:trebuchet_experiments_on_page].empty?

    # okay
    if request_opts[:trebuchet_experiments_on_page] &&
         !request_opts[:trebuchet_experiments_on_page].empty?

      add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
    end

    # bad - this is complex and deserves multiple lines and a comment
    # or better still, extract complex parts into methods
    parts[i] = part.to_i(INTEGER_BASE) if !part.nil? && [0, 2, 3].include?(i)

    # okay
    return if reconciled?
    ```

* <a name="no-unless-with-else"></a>Never use `unless` with `else`. Rewrite
    these with the positive case first.<sup>[[link](#no-unless-with-else)]</sup>

    ```ruby
    # bad
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # good
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* <a name="unless-with-multiple-conditions"></a>Avoid `unless` with multiple
    conditions.<sup>[[link](#unless-with-multiple-conditions)]</sup>

    ```ruby
      # bad
      unless foo? && bar?
        ...
      end

      # okay
      if !(foo? && bar?)
        ...
      end
    ```

* <a name="parens-around-conditions"></a>Don't use parentheses around the
    boolean expression of an `if/unless/while` if it's the only one.
    <sup>[[link](#parens-around-conditions)]</sup>

    ```ruby
    # bad
    if (x > 10)
      ...
    end

    # good
    if x > 10
      ...
    end

    ```

### Ternary operator

* <a name="avoid-complex-ternary"></a>Avoid the ternary operator (`?:`) except
    in cases where all expressions are extremely trivial. However, do use the
    ternary operator(`?:`) over `if/then/else/end` constructs for single line
    conditionals.<sup>[[link](#avoid-complex-ternary)]</sup>

    ```ruby
    # bad
    result = if some_condition then something else something_else end

    # good
    result = some_condition ? something : something_else
    ```

* <a name="no-nested-ternaries"></a>Use one expression per branch in a ternary
    operator. This also means that ternary operators must not be nested. Prefer
    `if/else` constructs in these cases.<sup>[[link](#no-nested-ternaries)]</sup>

    ```ruby
    # bad
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # good
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* <a name="single-condition-ternary"></a>Avoid multiple conditions in ternaries.
    Ternaries are best used with single conditions.
    <sup>[[link](#single-condition-ternary)]</sup>

* <a name="no-multiline-ternaries"></a>Avoid multi-line `?:` (the ternary
    operator), use `if/then/else/end` instead.
    <sup>[[link](#no-multiline-ternaries)]</sup>

    ```ruby
    # bad
    some_really_long_condition_that_might_make_you_want_to_split_lines ?
      something : something_else

    # good
    if some_really_long_condition_that_might_make_you_want_to_split_lines
      something
    else
      something_else
    end
    ```

## Syntax

* <a name="single-line-blocks"></a>Prefer `{...}` over `do...end` for
    single-line blocks.  Avoid using `{...}` for multi-line blocks (multiline
    chaining is always ugly). Always use `do...end` for "control flow" and
    "method definitions" (e.g. in Rakefiles and certain DSLs).  Avoid `do...end`
    when chaining.<sup>[[link](#single-line-blocks)]</sup>

    ```ruby
    names = ["Bozhidar", "Steve", "Sarah"]

    # good
    names.each { |name| puts name }

    # bad
    names.each do |name| puts name end

    # good
    names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

    # bad
    names.select do |name|
      name.start_with?("S")
    end.map { |name| name.upcase }
    ```

    Some will argue that multiline chaining would look okay with the use of
    `{...}` or `do...end`, but they should ask themselves if this code is really readable and
    whether the block's content can be extracted into nifty methods.

* <a name="self-assignment"></a>Use shorthand self assignment operators
    whenever applicable.<sup>[[link](#self-assignment)]</sup>

    ```ruby
    # bad
    x = x + y
    x = x * y
    x = x**y
    x = x / y
    x = x || y
    x = x && y

    # good
    x += y
    x *= y
    x **= y
    x /= y
    x ||= y
    x &&= y
    ```

* <a name="redundant-return"></a>Avoid `return` where not required.
    <sup>[[link](#redundant-return)]</sup>

    ```ruby
    # bad
    def some_method(some_arr)
      return some_arr.size
    end

    # good
    def some_method(some_arr)
      some_arr.size
    end
    ```

* <a name="lambda-calls"></a>Use `.call` explicitly when calling lambdas.
    <sup>[[link](#lambda-calls)]</sup>

    ```ruby
    # bad
    lambda.(x, y)

    # good
    lambda.call(x, y)
    ```

* <a name="single-action-blocks"></a>When a method block takes only one
    argument, and the body consists solely of reading an attribute or calling
    one method with no arguments, use the `&:` shorthand.
    <sup>[[link](#single-action-blocks)]</sup>

    ```ruby
    # bad
    bluths.map { |bluth| bluth.occupation }
    bluths.select { |bluth| bluth.blue_self? }

    # good
    bluths.map(&:occupation)
    bluths.select(&:blue_self?)
    ```

* <a name="redundant-self"></a>Prefer `some_method` over `self.some_method` when
    calling a method on the current instance.<sup>[[link](#redundant-self)]</sup>

    ```ruby
    # bad
    def end_date
      self.start_date + self.nights
    end

    # good
    def end_date
      start_date + nights
    end
    ```

    In the following three common cases, `self.` is required by the language
    and is good to use:

    1. When defining a class method: `def self.some_method`.
    2. The *left hand side* when calling an assignment method, including assigning
       an attribute when `self` is an ActiveRecord model: `self.guest = user`.
    3. Referencing the current instance's class: `self.class`.

## Naming

* <a name="snake-case"></a>Use `snake_case` for methods and variables.
    <sup>[[link](#snake-case)]</sup>

* <a name="camel-case"></a>Use `CamelCase` for classes and modules. (Keep
    acronyms like HTTP, RFC, XML uppercase.)
    <sup>[[link](#camel-case)]</sup>

* <a name="screaming-snake-case"></a>Use `SCREAMING_SNAKE_CASE` for other
    constants.<sup>[[link](#screaming-snake-case)]</sup>

* <a name="predicate-method-names"></a>The names of predicate methods (methods
    that return a boolean value) should end in a question mark.
    (i.e. `Array#empty?`).<sup>[[link](#predicate-method-names)]</sup>

* <a name="bang-methods"></a>Methods should end with a bang only if they
*   modify self in dangerous ways, or raise exceptions.
    <sup>[[link](#bang-methods)]</sup>

* <a name="throwaway-variables"></a>Name throwaway variables `_`.
    <sup>[[link](#throwaway-variables)]</sup>

    ```ruby
    payment, _ = Payment.complete_paypal_payment!(params[:token],
                                                  native_currency,
                                                  created_at)
    ```

## Classes

* <a name="avoid-class-variables"></a>Avoid the usage of class (`@@`) variables
    due to their "nasty" behavior in inheritance.
    <sup>[[link](#avoid-class-variables)]</sup>

    ```ruby
    class Parent
      @@class_var = 'parent'

      def self.print_class_var
        puts @@class_var
      end
    end

    class Child < Parent
      @@class_var = 'child'
    end

    Parent.print_class_var # => will print "child"
    ```

  As you can see all the classes in a class hierarchy actually share one
  class variable. Class instance variables should usually be preferred
  over class variables.

* <a name="singleton-methods"></a>Use `def self.method` to define singleton
    methods. This makes the methods more resistant to refactoring changes.
    <sup>[[link](#singleton-methods)]</sup>

    ```ruby
    class TestClass
      # bad
      def TestClass.some_method
        ...
      end

      # good
      def self.some_other_method
        ...
      end
    ```
* <a name="access-modifiers"></a>Indent the `public`, `protected`, and
    `private` methods as much the method definitions they apply to. Leave one
    blank line above and below them.<sup>[[link](#access-modifiers)]</sup>

    ```ruby
    class SomeClass
      def public_method
        # ...
      end

      private

      def private_method
        # ...
      end
    end
    ```

## Exceptions

* <a name="exception-flow-control"></a>Don't use exceptions for flow of control.
    <sup>[[link](#exception-flow-control)]</sup>

    ```ruby
    # bad
    begin
      n / d
    rescue ZeroDivisionError
      puts "Cannot divide by 0!"
    end

    # good
    if d.zero?
      puts "Cannot divide by 0!"
    else
      n / d
    end
    ```

* <a name="dont-rescue-exception"></a>Avoid rescuing the `Exception` class.
    <sup>[[link](#dont-rescue-exception)]</sup>

    ```ruby
    # bad
    begin
      # an exception occurs here
    rescue Exception
      # exception handling
    end

    # good
    begin
      # an exception occurs here
    rescue StandardError
      # exception handling
    end

    # acceptable
    begin
      # an exception occurs here
    rescue
      # exception handling
    end
    ```

* <a name="redundant-exception"></a>Don't specify `RuntimeError` explicitly in
    the two argument version of raise. Prefer error sub-classes for clarity and
    explicit error creation.<sup>[[link](#redundant-exception)]</sup>

    ```ruby
    # bad
    raise RuntimeError, 'message'

    # better - RuntimeError is implicit here
    raise 'message'

    # best
    class MyExplicitError < RuntimeError; end
    raise MyExplicitError
    ```

## Collections

To be continued...

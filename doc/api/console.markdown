# Console

    Stability: 2 - Stable

The module defines a `Console` class and exports a `console` object.

The `console` object is a special instance of `Console` whose output is
sent to stdout or stderr.

For ease of use, `console` is defined as a global object and can be used
directly without `require`.

## Class: Console

<!--type=class-->

Use `require('console').Console` or `console.Console` to access this class.

    var Console = require('console').Console;
    var Console = console.Console;

You can use the `Console` class to create a simple logger like `console` but
with different output streams.

### new Console(stdout[, stderr])

Create a new `Console` by passing one or two writable stream instances.
`stdout` is a writable stream to print log or info output. `stderr`
is used for warning or error output. If `stderr` isn't passed, the warning
and error output will be sent to the `stdout`.

    var output = fs.createWriteStream('./stdout.log');
    var errorOutput = fs.createWriteStream('./stderr.log');
    // custom simple logger
    var logger = new Console(output, errorOutput);
    // use it like console
    var count = 5;
    logger.log('count: %d', count);
    // in stdout.log: count 5

The global `console` is a special `Console` whose output is sent to
`process.stdout` and `process.stderr`:

    new Console(process.stdout, process.stderr);

## console

* {Object}

<!--type=global-->

For printing to stdout and stderr. Similar to the console object functions
provided by most web browsers, here the output is sent to stdout or stderr.

The console functions are synchronous when the destination is a terminal or
a file (to avoid lost messages in case of premature exit) and asynchronous
when it's a pipe (to avoid blocking for long periods of time).

That is, in the following example, stdout is non-blocking while stderr
is blocking:

    $ node script.js 2> error.log | tee info.log

Typically, the blocking/non-blocking dichotomy is not something you should
worry about unless you log huge amounts of data.

### console.assert(value[, message][, ...])

Similar to [`assert.ok()`][], but the error message is formatted as
`util.format(message...)`.

### console.dir(obj[, options])

Uses [`util.inspect()`][] on `obj` and prints the resulting string to stdout.
This function bypasses any custom `inspect()` function on `obj`. An optional
`options` object may be passed that alters certain aspects of the formatted
string:

- `showHidden` - if `true` then the object's non-enumerable and symbol
properties will be shown too. Defaults to `false`.

- `depth` - tells `inspect` how many times to recurse while formatting the
object. This is useful for inspecting large complicated objects. Defaults to
`2`. To make it recurse indefinitely, pass `null`.

- `colors` - if `true`, then the output will be styled with ANSI color codes.
Defaults to `false`. Colors are customizable; see
[customizing `util.inspect()` colors][].

### console.error([data][, ...])

Same as [`console.log()`][] but prints to stderr.

### console.info([data][, ...])

Same as [`console.log()`][].

### console.log([data][, ...])

Prints to stdout with newline. This function can take multiple arguments in a
`printf()`-like way:

    var count = 5;
    console.log('count: %d', count);
    // prints 'count: 5'

If formatting elements are not found in the first string then
[`util.inspect()`][] is used on each argument.  See [`util.format()`][] for more
information.

### console.time(label)

Starts a timer that can be used to compute the duration of an operation. Timers
are identified by a unique name. Use the same name when you call
[`console.timeEnd()`][] to stop the timer and output the elapsed time in
milliseconds. Timer durations are accurate to the sub-millisecond.

### console.timeEnd(label)

Stops a timer that was previously started by calling [`console.time()`][] and
prints the result to the console:

    console.time('100-elements');
    for (var i = 0; i < 100; i++) {
      ;
    }
    console.timeEnd('100-elements');
    // prints 100-elements: 225.438ms

### console.trace(message[, ...])

Print to stderr `'Trace :'`, followed by the formatted message and stack trace
to the current position.

### console.warn([data][, ...])

Same as [`console.error()`][].

[`assert.ok()`]: assert.html#assert_assert_value_message_assert_ok_value_message
[`console.error()`]: #console_console_error_data
[`console.log()`]: #console_console_log_data
[`console.time()`]: #console_console_time_label
[`console.timeEnd()`]: #console_console_timeend_label
[`util.format()`]: util.html#util_util_format_format
[`util.inspect()`]: util.html#util_util_inspect_object_options
[customizing `util.inspect()` colors]: util.html#util_customizing_util_inspect_colors

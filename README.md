# debouncer

An easy-to-use method call debouncer package for Dart/Flutter.

Debouncing is needed when there is a possibility of multiple calls to a method being made within a short duration of each other, and it's desirable that only the last of those calls actually invoke the target method.

So basically each call starts a timer, and if another call happens before the timer executes, the timer is reset and starts waiting for the desired duration again. When the timer finally does time out, the target method is invoked.

## Usage

#### Debouncing
Use the debouncer by calling `debounce`:

    Debouncer.debounce(
        'my-debouncer',                 // <-- An ID for this particular debouncer
        Duration(milliseconds: 500),    // <-- The debounce duration
        () => myMethod()                // <-- The target method
    );

The above call will invoke `myMethod()` after 500 ms, unless another call to `debounce()` with the same `tag` is made within 500 ms. A `tag` identifies this particular debouncer, which means you can have multiple different debouncers running concurrently and independent of each other.

#### Cancelling a debouncer

A debouncer which hasn't yet executed its target function can be called by calling `cancel()` with the debouncers `tag`:

    Debouncer.cancel('my-debouncer');

To cancel all active debouncers, call `cancelAll()`:

    Debouncer.cancelAll();


#### Counting active debouncers

You can get the number of active debouncers (debouncers which haven't yet executed their target methods) by calling `count()`:

    print('Active debouncers: ${Debouncer.count()}'); 


#### Fire a debouncer target function manually

If you need to fire the target function of a debouncer before the timer executes, you can call `fire()`:

    Debouncer.fire('my-debouncer');

This will execute the debouncers target function, but the debounce timer will keep running unless you also call `cancel()`.   
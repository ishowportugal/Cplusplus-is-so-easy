# Move me - answer

This code compiles and works, but it's not what you see.

If you hope to see "ctor" + "move" + "move", you would be surprised.
Calling `foo` actually creates a copy instead of moving the object.

Fix: add `mutable` to lambda.
Since lambda is not mutable, it cannot change `big` object.

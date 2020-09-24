# Jerry

Jerry is not as smart as Rick or Beth, however, he can explain what those two
are all about... Take a look!



## Basics

For the time being, SmallO is an assembly-like language that runs in a VM. It
was initially created to be simple and easy to learn. Its type system only has
two types: `integer` and `string` both of which can be interpreted as `boolean`.



## Repos

SmallO consists of multiple different programs, each with its own mission.

- [Beth] can run your programs written in SmallO assembly and its only
dependency is Python3 standard library;
- [Morty] is a snappy and lightweight assembler written in Python3;
- [Rick] is a reliable and ultra-fast VM that executes bytecode produced by
*Morty*.

[Beth]: https://github.com/smallo-lang/Beth
[Morty]: https://github.com/smallo-lang/Morty
[Rick]: https://github.com/smallo-lang/Rick


### Beth

*Beth* can be used as an all-in-one solution for those who want to try SmallO
and aren't too conserned with its execution speed. Her only dependency is
[Python3](https://www.python.org/) which is nice: installation takes seconds
(especially for those on MacOS or Linux).


### Morty

*Morty* is just a dull kid on his own, however, some real magic happens when he
is paired up with *Rick*! *Morty* takes SmallO assembly and compiles it into
bytecode that can be executed by *Rick*. *Morty* is written in Python3, so he is
not as fast as *Rick*, nevertheless, he allows his grandpa to unleash his genius
as *Rick's* execution time is many times faster than that of *Beth*.


### Rick

*Rick* is an ultra-fast VM written in [Rust](https://www.rust-lang.org/) that
executes bytecode produced by *Morty*. Use it when performance matters.

# Jerry

Jerry is not as smart as Rick or Beth, however, he can explain what those two
are all about... Take a look!



## Redesign Proposal

As of now, SmallO is incapable of any sort of iterative behaviour because it does
not support composite data structures of any kind. It would be possible to copy
the way real computers work with memory through a system of addresses, but this
approach requires a lot of work.

I think that the best way to integrate iteration into SmallO is by using stack
variables. Something like this:

```smallo
bin_add:
  add a a a     @ pops two numbers from `a`, adds them, and
                @ stores result back in `a` using `push`
  back

  put 5 a       @ `a` is a variable implemented as a stack
  put 37 a      @ thus, you can push multiple values onto it

fold_add:
  len a l
  gth l 1 b 
  jmpf b result @ show result if we've gotten to 1 element
  br b bin_add  @ call `bin_add` if `a` has more than one element
   
result:
  empty a b
  jmpt b error
  out "The sum is: "
  outl a
  end

error:
  err "'a' is empty -- can't show result" 1
```



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



## Theory

### Type System

SmallO supports two simple types: `integer` and `string` where `integer` also
serves as `boolean`. The `string` type can be interpreted as `boolean` using its
length (empty `string` gives `false`, non-empty one gives `true`).


### General Operational Principles

SmallO supports two syntactic structures: *instruction* and *label*. I believe
these are self-explanatory. Instructions differ in terms of their operand number
such that there are methods that don't need any operands (e.g. `end`) while some
take up to 3 operands (normally two values and a variable to store the result).


### Operations

#### Instruction Set

```asm
@ assignment
put val var

@ binary integer operations
    @ arithmetic
add # # var
sub # # var
mul # # var
div # # var
mod # # var
    @ comparisons
gth # # var         @ greater than
lth # # var         @ less than
geq # # var         @ greater than or equal to
leq # # var         @ less than or equal to

@ binary general operations
eq val val var      @ equality check (type-crytical)
neq val val var     @ inequality check (type-crytical)

@ I/O operations
ini var             @ input integer (type-crytical)
ins var             @ input string (type-crytical)
out val             @ output value (type-blind)
outl val            @ equivalent to out val + nl
nl                  @ print newline

@ string operations
con val val var     @ concatenate two values as strings (type-blind)
sti $ var           @ string-to-integer conversion

@ boolean operations
not val var         @ unary logical not
and val val var     @ binary logical and
or val val var      @ binary logical or

@ labels
jump_location:

@ includes
>"func.so"

@ control flow
jump *              @ unconditional jump
jmpt var *          @ jump if val is true (type-blind)
jmpf var *          @ jump if val is false (type-blind)

br *                @ unconditional branch (like jump but jump location saved)
brt var *           @ branch if val is true (type-blind)
brf var *           @ branch if val is false (type-blind)
back                @ return to previous branch point

err $ #             @ exit program with error message and exit code int
end                 @ exit program
```

#### Symbol Map

| Symbol | Meaning             |
|:------:|:--------------------|
| *      | label identifier    |
| #      | integer             |
| $      | string              |
| var    | variable identifier |
| val    | type-blind value    |
| @      | comment             |

> The `val` represents constant literal (`#` or `$`) or variable identifier
> (`var`). It's used in commands that support auto-conversion.

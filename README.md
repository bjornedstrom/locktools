locktools - locksmithing / lock picking tools
=============================================

This is my repository for code and resources useful for locksmithing
and lock picking. It's written for academic use only.

Programs
--------

`lock-rekey` is a work in progress tool that will, given a key
bitting, pin lengths and (optionally) master pin lengths, enumerate
all possible ways to rekey a pin-tumbler lock.

Note that this is not a master-keying system - it only accepts a
single key/bitting. Though it is highly useful if you disassemble a
lock that's master keyed and you want to reassemble it later. You use
the program like this:

    $ lock-rekey BITTING KEY-PINS [MASTER-PINS]

Where the three params are s-expressions for the pin configurations
(see Notations below).

    $ lock-rekey "(3 3 0)" "(6 6 9)"
    ((3 6) (3 6) (0 9))

    $ lock-rekey "(3 3 0 0)" "(8 7 6 6)" "(1 2)"
    ((3 6) (3 6) (0 7 2) (0 8 1))
    ((3 6) (3 6) (0 8 1) (0 7 2))

In the last example, the 4 pin stacks all sum to 9, which lies at a
valid shear line for this particular configuration (note that the
program does not care about the cylinder height, it will output all
possible configurations).

Notations
---------

Key pins, driver pins and master key pins are represented by a single
integer per pin, for it's height. You may have a lock with the five
key pins (6 6 6 7 7), for example.

My notation for key bitting is not as obvious. What you want to do is
represent the bitting of the key as a *height*. Specically, the
*deepest* cut in the key is said to have height 0.

When you measure your key bitting, you may want to do so the "natural"
way of measuring the height of the *cut*. Having done that, simply
normalize then invert the numbers. For example, if the cuts have depth
(1 1 3 2) then the inverse, which is used by my programs, are
(2 2 0 1) (normalize to 0 first, then flip).

Author / License
----------------

Björn Edström 2012 <be@bjrn.se>
See LICENSE for copyright

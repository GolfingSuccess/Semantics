# brainfuck (30000 8-bit cells)

brainfuck can be represented as this computer:

```
 ┌────┐ ┌─────────┐ ┌──────┐
 │Code├─┤         ├─┤Output│
 └────┘ │brainfuck│ └──────┘
┌─────┐ │computer │ ┌─────┐
│Input├─┤         ├─┤Error│
└─────┘ └─────────┘ └─────┘
```

`Code` is a sequence of symbols, where each symbol is one of `+-<>[],.`. `Input` is a sequence of bytes. The two sequences (inputs) are fed into `brainfuck computer`, which translates the inputs into an output, which is fed to `Output`, and possibly an error, which is fed to `Error`. Here are the details of `brainfuck computer`:

```
        ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
 ┌────┐ ┃ ┌───────────────────────┐ ┃ ┌────────┐
 │Code├─╂─┤I         IP           │ ╂─┤O Output│
 └────┘ ┃ └┬──┬───┬──┬──┬──┬──┬──┬┘ ┃ └────────┘
        ┃ ┌┴┐┌┴┐ ┌┴┐┌┴┐┌┴┐┌┴┐ │  │  ┃
        ┃ │+││-│ │<││>││[││]│ │  │  ┃
        ┃ └┬┘└┬┘ └┬┘└┬┘└┬┘└┬┘ │  │  ┃
┌─────┐ ┃  │┌─┘   │  │  │  │ ┌┴┐┌┴─┐┃
│Input├─╂──┼┼─────┼──┼──┼──┼─┤,││. │┃
└─────┘ ┃  ││     │  │  │  │ └┬┘└┬┬┘┃
        ┃  ││  ┌──┼──┼──┼──┼──┘  ││ ┃
        ┃  ││┌─┼──┼──┼──┼──┼─────┘│ ┃
        ┃  │││┌┼──┼──┼──┼──┼──────┘ ┃
        ┃ ┌┴┴┴┴┴┐┌┴──┴┐┌┴──┴┐       ┃
        ┃ │+-OOI││L  R││+  -│       ┃
        ┃ │  RW ││    ││    │       ┃
        ┃ │     ││Tape││Loop│       ┃
        ┃ │Tape ││Rot ││Ctrl│       ┃
        ┃ │R/W  │└────┘└────┘       ┃ ┌───────┐
        ┃ └─────┘                   ╂─┤± Error│
        ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ └───────┘
```

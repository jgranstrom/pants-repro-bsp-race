Reproduced on MacOS (Sonoma), ARM (M2)

How I repro:

#### Setup:
- Clone repo
- `pants experimental-bsp`
- Open in intellij with BSP enabled (New -> from existing sources -> BSP)

#### Repro _(Is flaky so might require a couple of tries)_:
- From the BSP tool window in IntelliJ use "refresh" to trigger writing the dependency jars to `.pants.d/bsp/jvm/resolves/jvm-default/lib/`
- Remove one or more of these jars then try to refresh again, for example `rm -r .pants.d/bsp/jvm/resolves/jvm-default/lib/`
- Loop above 2 steps until it reproduces

When it breaks it will error in Intellij with `Permission denied (os error 13)` on writing some of the jars. And a random mix of the files in `.pants.d/bsp/jvm/resolves/jvm-default/lib/` will be read-only and not.

For me it is probably around 50%, but it can work 5 times in a row, then break 7 times in a row etc.

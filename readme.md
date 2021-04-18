
# Virtualice VM

Stack based vm for super fast execution.
Supports threads, exceptions, and kernel extensions.

### Instruction Set

We are currently working on this.
The instruction set is 

``` asm

; halt, rest:

	halt
	rest              ; no operation

; push, pop, cast:

	push.[b|w|d|q]    ; push n bytes
	push.z            ; push 0
	push.o            ; push 1
	pop               ; pop a value
	pop.n [number]    ; pop n values
	top               ; duplicates stack top
	cast.[b|w|d|q]    ; value casting with size

; arithmetics: (i = int, f = float)

	add.[i|f]
	sub.[i|f]
	mul.[i|f]
	div.[i|f]
	mod.[i|f]

	inc.[i|f]
	dec.[i|f]

; bitwise: (l = left, r = right)

	xand | nor
	xor
	nand
	and
	or
	not
	inv
	negate

	shift.[l|r]    [number]
	rotate.[l|r]   [number]

; variables: (l = local, g = global, a = argument)

	get.[l|g|a] [variable index]
	set.[l|g|a] [variable index]

; functions, threads, exceptions:

	call     [address]
	kernel   [code]     ; syscall
	return

	fork     [address]
	join                ; will not work in locks
	abort               ; same as join but works in locks
	abort.t             ; stops thread t
	lock                ; locks the execution
	release             ; releases the execution
	wait.t              ; wait for thread t to finish
	wait.a              ; wait for all threads to finish
	wait.s              ; wait for some thread to finish
	sleep    [ms]

	throw               ; like return (sets exception flag)
	catch    [address]  ; like jump on exception (resets flag)

; jumps:

	jump [address]
	jump.[t|f|e|n|ge|le|g|l] [address]

```
# Bomb Lab Phase 1
To defuse the bomb, we need to find the correct input for the phase 1.
## Defuse
### Find the Phase 1 Function
In dumped files,
```asm
0000000000400ee0 <phase_1>:
  400ee0:	    48 83 ec 08          	sub    $0x8,%rsp
  400ee4:	    be 00 24 40 00       	mov    $0x402400,%esi
  400ee9:	    e8 4a 04 00 00       	call   401338 <strings_not_equal>
  400eee:	    85 c0                	test   %eax,%eax
  400ef0:	/-- 74 05                	je     400ef7 <phase_1+0x17>
  400ef2:	|   e8 43 05 00 00       	call   40143a <explode_bomb>
  400ef7:	\-> 48 83 c4 08          	add    $0x8,%rsp
  400efb:	    c3                   	ret
```
With GDB,
```bash
# gdb bomb
(gdb) disas phase_1
Dump of assembler code for function phase_1:
   0x0000000000400ee0 <+0>:     sub    $0x8,%rsp
   0x0000000000400ee4 <+4>:     mov    $0x402400,%esi
   0x0000000000400ee9 <+9>:     call   0x401338 <strings_not_equal>
   0x0000000000400eee <+14>:    test   %eax,%eax
   0x0000000000400ef0 <+16>:    je     0x400ef7 <phase_1+23>
   0x0000000000400ef2 <+18>:    call   0x40143a <explode_bomb>
   0x0000000000400ef7 <+23>:    add    $0x8,%rsp
   0x0000000000400efb <+27>:    ret
End of assembler dump.
```

### Set breakpoints & Run
```bash
(gdb) break phase_1  # Set breakpoint at phase_1
(gdb) run
...
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
...
(gdb) stepi  # Step into the phase_1 function
# ...until the function <strings_not_equal> is called
...
(gdb) x/s 0x402400  # Print the value of esi
...
{ANSWER}
```

### Save the answer
```bash
echo {ANSWER} >> input
```

### Input the answer
<details>
<summary>🚨 Spoiler Alert! 🚨</summary>

```
Border relations with Canada have never been better.
```
</details>

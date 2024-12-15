# Bomb Lab Phase 2
To defuse the bomb, we need to find the correct input for the phase 1.
## Defuse
### Find the Phase 2 Function
In dumped files,
```asm
0000000000400efc <phase_2>:
  400efc:	          55                   	push   %rbp
  400efd:	          53                   	push   %rbx
  400efe:	          48 83 ec 28          	sub    $0x28,%rsp
  400f02:	          48 89 e6             	mov    %rsp,%rsi
  400f05:	          e8 52 05 00 00       	call   40145c <read_six_numbers>
  400f0a:	          83 3c 24 01          	cmpl   $0x1,(%rsp)
  400f0e:	   /----- 74 20                	je     400f30 <phase_2+0x34>
  400f10:	   |      e8 25 05 00 00       	call   40143a <explode_bomb>
  400f15:	   +----- eb 19                	jmp    400f30 <phase_2+0x34>
  400f17:	/--|----> 8b 43 fc             	mov    -0x4(%rbx),%eax
  400f1a:	|  |      01 c0                	add    %eax,%eax
  400f1c:	|  |      39 03                	cmp    %eax,(%rbx)
  400f1e:	|  |  /-- 74 05                	je     400f25 <phase_2+0x29>
  400f20:	|  |  |   e8 15 05 00 00       	call   40143a <explode_bomb>
  400f25:	|  |  \-> 48 83 c3 04          	add    $0x4,%rbx
  400f29:	|  |      48 39 eb             	cmp    %rbp,%rbx
  400f2c:	+--|----- 75 e9                	jne    400f17 <phase_2+0x1b>
  400f2e:	|  |  /-- eb 0c                	jmp    400f3c <phase_2+0x40>
  400f30:	|  \--|-> 48 8d 5c 24 04       	lea    0x4(%rsp),%rbx
  400f35:	|     |   48 8d 6c 24 18       	lea    0x18(%rsp),%rbp
  400f3a:	\-----|-- eb db                	jmp    400f17 <phase_2+0x1b>
  400f3c:	      \-> 48 83 c4 28          	add    $0x28,%rsp
  400f40:	          5b                   	pop    %rbx
  400f41:	          5d                   	pop    %rbp
  400f42:	          c3                   	ret
```
With GDB,
```bash
# gdb bomb
(gdb) disas phase_2
Dump of assembler code for function phase_2:
   0x0000000000400efc <+0>:     push   %rbp
   0x0000000000400efd <+1>:     push   %rbx
   0x0000000000400efe <+2>:     sub    $0x28,%rsp
   0x0000000000400f02 <+6>:     mov    %rsp,%rsi
   0x0000000000400f05 <+9>:     call   0x40145c <read_six_numbers>
   0x0000000000400f0a <+14>:    cmpl   $0x1,(%rsp)
   0x0000000000400f0e <+18>:    je     0x400f30 <phase_2+52>
   0x0000000000400f10 <+20>:    call   0x40143a <explode_bomb>
   0x0000000000400f15 <+25>:    jmp    0x400f30 <phase_2+52>
...(more code)
End of assembler dump.
```

### Set breakpoints & Run
```bash
(gdb) break phase_2  # Set breakpoint at phase_2
(gdb) run
...
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
...
(gdb) stepi  # Step into the phase_2 function
# refer the function <read_six_numbers> and check `add` instruction
...
(gdb) x/s p $eax  # Print the value of eax
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
1 2 4 8 16 32
```
</details>


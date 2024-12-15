# Bomb Lab Phase 3
To defuse the bomb, we need to find the correct input for the phase 1.
## Defuse
### Find the Phase 3 Function
In dumped files,
```asm
0000000000400f43 <phase_3>:
  400f43:	       48 83 ec 18          	sub    $0x18,%rsp
  400f47:	       48 8d 4c 24 0c       	lea    0xc(%rsp),%rcx
  400f4c:	       48 8d 54 24 08       	lea    0x8(%rsp),%rdx
  400f51:	       be cf 25 40 00       	mov    $0x4025cf,%esi
  400f56:	       b8 00 00 00 00       	mov    $0x0,%eax
  400f5b:	       e8 90 fc ff ff       	call   400bf0 <__isoc99_sscanf@plt>
  400f60:	       83 f8 01             	cmp    $0x1,%eax
  400f63:	   /-- 7f 05                	jg     400f6a <phase_3+0x27>
  400f65:	   |   e8 d0 04 00 00       	call   40143a <explode_bomb>
  400f6a:	   \-> 83 7c 24 08 07       	cmpl   $0x7,0x8(%rsp)
  400f6f:	/----- 77 3c                	ja     400fad <phase_3+0x6a>
  400f71:	|      8b 44 24 08          	mov    0x8(%rsp),%eax
  400f75:	|      ff 24 c5 70 24 40 00 	jmp    *0x402470(,%rax,8)
  400f7c:	|      b8 cf 00 00 00       	mov    $0xcf,%eax
  400f81:	|  /-- eb 3b                	jmp    400fbe <phase_3+0x7b>
  400f83:	|  |   b8 c3 02 00 00       	mov    $0x2c3,%eax
  400f88:	|  +-- eb 34                	jmp    400fbe <phase_3+0x7b>
  400f8a:	|  |   b8 00 01 00 00       	mov    $0x100,%eax
  400f8f:	|  +-- eb 2d                	jmp    400fbe <phase_3+0x7b>
  400f91:	|  |   b8 85 01 00 00       	mov    $0x185,%eax
  400f96:	|  +-- eb 26                	jmp    400fbe <phase_3+0x7b>
  400f98:	|  |   b8 ce 00 00 00       	mov    $0xce,%eax
  400f9d:	|  +-- eb 1f                	jmp    400fbe <phase_3+0x7b>
  400f9f:	|  |   b8 aa 02 00 00       	mov    $0x2aa,%eax
  400fa4:	|  +-- eb 18                	jmp    400fbe <phase_3+0x7b>
  400fa6:	|  |   b8 47 01 00 00       	mov    $0x147,%eax
  400fab:	|  +-- eb 11                	jmp    400fbe <phase_3+0x7b>
  400fad:	\--|-> e8 88 04 00 00       	call   40143a <explode_bomb>
  400fb2:	   |   b8 00 00 00 00       	mov    $0x0,%eax
  400fb7:	   +-- eb 05                	jmp    400fbe <phase_3+0x7b>
  400fb9:	   |   b8 37 01 00 00       	mov    $0x137,%eax
  400fbe:	   \-> 3b 44 24 0c          	cmp    0xc(%rsp),%eax
  400fc2:	   /-- 74 05                	je     400fc9 <phase_3+0x86>
  400fc4:	   |   e8 71 04 00 00       	call   40143a <explode_bomb>
  400fc9:	   \-> 48 83 c4 18          	add    $0x18,%rsp
  400fcd:	       c3                   	ret
```
With GDB,
```bash
# gdb bomb
(gdb) disas phase_3
Dump of assembler code for function phase_3:
   0x0000000000400f43 <+0>:     sub    $0x18,%rsp
   0x0000000000400f47 <+4>:     lea    0xc(%rsp),%rcx
   0x0000000000400f4c <+9>:     lea    0x8(%rsp),%rdx
   0x0000000000400f51 <+14>:    mov    $0x4025cf,%esi
   0x0000000000400f56 <+19>:    mov    $0x0,%eax
   0x0000000000400f5b <+24>:    call   0x400bf0 <__isoc99_sscanf@plt>    
   0x0000000000400f60 <+29>:    cmp    $0x1,%eax
   0x0000000000400f63 <+32>:    jg     0x400f6a <phase_3+39>
   0x0000000000400f65 <+34>:    call   0x40143a <explode_bomb>
   0x0000000000400f6a <+39>:    cmpl   $0x7,0x8(%rsp)
   0x0000000000400f6f <+44>:    ja     0x400fad <phase_3+106>
   0x0000000000400f71 <+46>:    mov    0x8(%rsp),%eax
   0x0000000000400f75 <+50>:    jmp    *0x402470(,%rax,8)
   0x0000000000400f7c <+57>:    mov    $0xcf,%eax
   0x0000000000400f81 <+62>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400f83 <+64>:    mov    $0x2c3,%eax
   0x0000000000400f88 <+69>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400f8a <+71>:    mov    $0x100,%eax
   0x0000000000400f8f <+76>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400f91 <+78>:    mov    $0x185,%eax
   0x0000000000400f96 <+83>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400f98 <+85>:    mov    $0xce,%eax
   0x0000000000400f9d <+90>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400f9f <+92>:    mov    $0x2aa,%eax
   0x0000000000400fa4 <+97>:    jmp    0x400fbe <phase_3+123>
   0x0000000000400fa6 <+99>:    mov    $0x147,%eax
   0x0000000000400fab <+104>:   jmp    0x400fbe <phase_3+123>
   0x0000000000400fad <+106>:   call   0x40143a <explode_bomb>
   0x0000000000400fb2 <+111>:   mov    $0x0,%eax
   0x0000000000400fb7 <+116>:   jmp    0x400fbe <phase_3+123>
   0x0000000000400fb9 <+118>:   mov    $0x137,%eax
   0x0000000000400fbe <+123>:   cmp    0xc(%rsp),%eax
   0x0000000000400fc2 <+127>:   je     0x400fc9 <phase_3+134>
   0x0000000000400fc4 <+129>:   call   0x40143a <explode_bomb>
   0x0000000000400fc9 <+134>:   add    $0x18,%rsp
   0x0000000000400fcd <+138>:   ret
End of assembler dump.
```

### Set breakpoints & Run
```bash
(gdb) break phase_3  # Set breakpoint at phase_3
(gdb) run
...
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
...
(gdb) stepi  # Step into the phase_3 function
# refer the function <read_six_numbers> and check `add` instruction
...
(gdb) p $eax  # Print the value of eax

# check out the switch instruction
(gdb) p 0x???
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
7 327
```
</details>


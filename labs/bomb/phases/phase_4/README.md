# Bomb Lab Phase 4
To defuse the bomb, we need to find the correct input for the phase 4.
## Defuse
### Find the Phase 4 Function
In dumped files,
`phase_4`
```asm
000000000040100c <phase_4>:
  40100c:	       48 83 ec 18          	sub    $0x18,%rsp
  401010:	       48 8d 4c 24 0c       	lea    0xc(%rsp),%rcx
  401015:	       48 8d 54 24 08       	lea    0x8(%rsp),%rdx
  40101a:	       be cf 25 40 00       	mov    $0x4025cf,%esi
  40101f:	       b8 00 00 00 00       	mov    $0x0,%eax
  401024:	       e8 c7 fb ff ff       	call   400bf0 <__isoc99_sscanf@plt>
  401029:	       83 f8 02             	cmp    $0x2,%eax
  40102c:	/----- 75 07                	jne    401035 <phase_4+0x29>
  40102e:	|      83 7c 24 08 0e       	cmpl   $0xe,0x8(%rsp)
  401033:	|  /-- 76 05                	jbe    40103a <phase_4+0x2e>
  401035:	\--|-> e8 00 04 00 00       	call   40143a <explode_bomb>
  40103a:	   \-> ba 0e 00 00 00       	mov    $0xe,%edx
  40103f:	       be 00 00 00 00       	mov    $0x0,%esi
  401044:	       8b 7c 24 08          	mov    0x8(%rsp),%edi
  401048:	       e8 81 ff ff ff       	call   400fce <func4>
  40104d:	       85 c0                	test   %eax,%eax
  40104f:	/----- 75 07                	jne    401058 <phase_4+0x4c>
  401051:	|      83 7c 24 0c 00       	cmpl   $0x0,0xc(%rsp)
  401056:	|  /-- 74 05                	je     40105d <phase_4+0x51>
  401058:	\--|-> e8 dd 03 00 00       	call   40143a <explode_bomb>
  40105d:	   \-> 48 83 c4 18          	add    $0x18,%rsp
  401061:	       c3                   	ret
```
`func4`
```asm
0000000000400fce <func4>:
  400fce:	/-------> 48 83 ec 08          	sub    $0x8,%rsp
  400fd2:	|         89 d0                	mov    %edx,%eax
  400fd4:	|         29 f0                	sub    %esi,%eax
  400fd6:	|         89 c1                	mov    %eax,%ecx
  400fd8:	|         c1 e9 1f             	shr    $0x1f,%ecx
  400fdb:	|         01 c8                	add    %ecx,%eax
  400fdd:	|         d1 f8                	sar    $1,%eax
  400fdf:	|         8d 0c 30             	lea    (%rax,%rsi,1),%ecx
  400fe2:	|         39 f9                	cmp    %edi,%ecx
  400fe4:	|     /-- 7e 0c                	jle    400ff2 <func4+0x24>
  400fe6:	|     |   8d 51 ff             	lea    -0x1(%rcx),%edx
  400fe9:	+-----|-- e8 e0 ff ff ff       	call   400fce <func4>
  400fee:	|     |   01 c0                	add    %eax,%eax
  400ff0:	|  /--|-- eb 15                	jmp    401007 <func4+0x39>
  400ff2:	|  |  \-> b8 00 00 00 00       	mov    $0x0,%eax
  400ff7:	|  |      39 f9                	cmp    %edi,%ecx
  400ff9:	|  +----- 7d 0c                	jge    401007 <func4+0x39>
  400ffb:	|  |      8d 71 01             	lea    0x1(%rcx),%esi
  400ffe:	\--|----- e8 cb ff ff ff       	call   400fce <func4>
  401003:	   |      8d 44 00 01          	lea    0x1(%rax,%rax,1),%eax
  401007:	   \----> 48 83 c4 08          	add    $0x8,%rsp
  40100b:	          c3                   	ret
```

### Set breakpoints & Run
```bash
(gdb) break phase_4  # Set breakpoint at phase_4
(gdb) run
...
Welcome to my fiendish little bomb. You have 6 phases with
which to blow yourself up. Have a nice day!
Phase 1 defused. How about the next one?
Halfway there!
...
(gdb) stepi  # Step into the phase_4 function
...
(gdb) x/s 0x4025cf  # Print the value of esi
(gdb) p $eax  # Print the value of eax
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
7 0
```
</details>


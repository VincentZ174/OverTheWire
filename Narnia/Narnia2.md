Terminal  
===  
```  
ssh narnia2@narnia.labs.overthewire.org  
narnia2@narnia.labs.overthewire.org's password: nairiepecu <enter>  
narnia2@melinda:~$ cd /narnia  
narnia2@melinda:/narnia$ cat narnia2.c
/*
    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program; if not, write to the Free Software
    Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
*/
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char * argv[]){
	char buf[128];

	if(argc == 1){
		printf("Usage: %s argument\n", argv[0]);
		exit(1);
	}
	strcpy(buf,argv[1]);
	printf("%s", buf);

	return 0;
}  
narnia2@melinda:/narnia$ gdb -q ./narnia2  
Reading symbols from ./narnia2...(no debugging symbols found)...done.  
(gdb) disass main
Dump of assembler code for function main:
   0x0804845d <+0>:	push   %ebp
   0x0804845e <+1>:	mov    %esp,%ebp
   0x08048460 <+3>:	and    $0xfffffff0,%esp
   0x08048463 <+6>:	sub    $0x90,%esp
   0x08048469 <+12>:	cmpl   $0x1,0x8(%ebp)
   0x0804846d <+16>:	jne    0x8048490 <main+51>
   0x0804846f <+18>:	mov    0xc(%ebp),%eax
   0x08048472 <+21>:	mov    (%eax),%eax
   0x08048474 <+23>:	mov    %eax,0x4(%esp)
   0x08048478 <+27>:	movl   $0x8048560,(%esp)
   0x0804847f <+34>:	call   0x8048310 <printf@plt>
   0x08048484 <+39>:	movl   $0x1,(%esp)
   0x0804848b <+46>:	call   0x8048340 <exit@plt>
   0x08048490 <+51>:	mov    0xc(%ebp),%eax
   0x08048493 <+54>:	add    $0x4,%eax
   0x08048496 <+57>:	mov    (%eax),%eax
   0x08048498 <+59>:	mov    %eax,0x4(%esp)
   0x0804849c <+63>:	lea    0x10(%esp),%eax
   0x080484a0 <+67>:	mov    %eax,(%esp)
   0x080484a3 <+70>:	call   0x8048320 <strcpy@plt>
   0x080484a8 <+75>:	lea    0x10(%esp),%eax
   0x080484ac <+79>:	mov    %eax,0x4(%esp)
   0x080484b0 <+83>:	movl   $0x8048574,(%esp)
   0x080484b7 <+90>:	call   0x8048310 <printf@plt>
   0x080484bc <+95>:	mov    $0x0,%eax
---Type <return> to continue, or q <return> to quit---
   0x080484c1 <+100>:	leave  
   0x080484c2 <+101>:	ret    
End of assembler dump.  

```

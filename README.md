## sym.h

Address symbolization C library in a single file. 

Currently only support ELF format.

### Usage

Clone the repo

```bash
git clone https://github.com/Sberm/sym.h.git
```

Example

```c
#include "sym.h"

int pids[] = {32930, 1132, 328};
int pid_nr = 3;

struct ksyms* ksym_tb = ksym_load(); // kernel symbol
struct usyms* usym_tb = usym_load(pids, pid_nr); // user symbol

char ksym[128];
char usym[128];

ksym_addr_to_sym(ksym_tb, 0xffffffff9a143183, ksym);
usym_addr_to_sym(usym_tb, 0x55e8c4de0ef7, usym);

printf("%s\n", ksym); // do_filp_open
printf("%s\n", usym); // ngx_hash_init

/*
 * or
 */
char sym[128];
unsigned long addr = 0xffffffff9a143183;
addr_to_sym(ksym_tb, usym_tb, addr, sym);
printf("%s\n", sym); // ngx_hash_init

ksym_free(ksym_tb);
usym_free(usym_tb);
```

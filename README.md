## sym.h

Address symbolization C library in a single file.

### usage

```c
/* include this header file */
#include "sym.h"

/* pids to fetch symbols from(for user space symbols)*/
int pids[] = {32930, 1132, 328};
int num_of_pids = 3;


/* symbol table loading */
/* kernel symbol table */
const struct ksyms* ksym_tb = ksym_load();
/* user symbol table, of certain pids */
const struct usyms* usym_tb = usym_load(pids, num_of_pids);

/* symbolization */
char ksym[128];
char usym[128];

ksym_addr_to_sym(usym_tb, 0xffffffff9a143183, ksym);
usym_addr_to_sym(usym_tb, 0x55e8c4de0ef7, usym);

/* result */
printf("%s\n", ksym); // do_filp_open+0x93
printf("%s\n", usym); // ngx_hash_init+0x2b7
```

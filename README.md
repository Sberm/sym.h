## sym.h

Address symbolization C library in a single file.

### Usage

Clone the repo

```bash
git clone https://github.com/Sberm/sym.h.git
```

Example

```c
/* include this header file */
#include "sym.h"

/* pids to fetch symbols from(for user space symbols)*/
int pids[] = {32930, 1132, 328};
int num_of_pids = 3;

/* symbol table loading */
const struct ksyms* ksym_tb = ksym_load(); // kernel symbol table
const struct usyms* usym_tb = usym_load(pids, num_of_pids); // user symbol table, of certain pids

/* symbolization */
char ksym[128];
char usym[128];

ksym_addr_to_sym(ksym_tb, 0xffffffff9a143183, ksym);
usym_addr_to_sym(usym_tb, 0x55e8c4de0ef7, usym);

/* result */
printf("%s\n", ksym); // do_filp_open
printf("%s\n", usym); // ngx_hash_init

/* free symbol table's memory */
ksym_free(ksym_tb);
usym_free(usym_tb);
```

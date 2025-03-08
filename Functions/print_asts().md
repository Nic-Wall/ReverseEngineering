```source
void print_asts(int n){
	for(int i = 0; i < n; i++) {
		putchar('*');
	}
	printf("\n");
}
```

```Ghidra
void print_asts(int param_1)

{
  undefined4 local_c;
  
  for (local_c = 0; local_c < param_1; local_c = local_c + 1) {
    putchar(0x2a);
  }
  putchar(10);
  return;
}
```

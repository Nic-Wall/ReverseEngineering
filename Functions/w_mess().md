```source
void w_mess() {
	print_asts(32);
	printf("*****    W E L C O M E    *****\n");
	print_asts(32);
	printf("**    Your task is to find    **\n");
	printf("** the secret, changing, code **\n");
	print_asts(32);
	printf("\nRules:\n1. No brute forcing\n");
}
```

```Ghidra
void w_mess(void)

{
	print_asts(0x20);
	puts("*****    W E L C O M E    *****");
	print_asts(0x20);
	puts("**    Your task is to find    **);
	puts("** the secret, changing, code **);
	print_asts(0x20);
	puts("\nRules: \n1. No brute forcing");
	return;
}
```
```source
int main() {
	w_mess();
	
	printf("\nSecret Changing Code: ");
	scanf("%d", &user_input);
	
	if(compare(user_input)) {
		s_mess();
	}
	else {
		f_mess();
	}
	return 0;
} 
```

```Ghidra
undefined8 main(void)

{
	int iVar1;

	w_mess();
	print("\nSecret Changing Code: ");
	__isoc99_scanf(&DAT_00102020, &user_input);
	iVar1 = compare(user_input);
	if(iVar1 == 0) {
		f_mess();
	}
	else {
		s_mess();
	}
	return 0;
}
```


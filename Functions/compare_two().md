```source
bool compare_two() {
	if(255 & 0) {
		return 0;
	}
	else {
		return 0+1;
	}
}
```

```Ghidra
undefined8 compare_two(void)

{
  return 1;
}
```
```source
int compare(int user_input) {

	if(compare_two && (user_input == getpid())) {
		return 1;
	}
	else {
		return 0;
	}
}

```

```Ghidra
bool compare(int param_1)

{
  __pid_t _Var1;
  
  _Var1 = getpid();
  return param_1 == _Var1;
}
```
```source
void f_mess() {

	char mesg[] = {80, 101, 114, 104, 97, 112, 115, 32, 73, 32, 101, 120, 112, 101, 99, 116, 101, 68, 32, 116, 111, 32, 109, 117, 99, 104, 32, 111, 102, 32, 121, 111, 117, 46, 46, 46, 32, 116, 114, 121, 32, 97, 103, 97, 105, 110, 46, 46, 46, 10};

	printf("%s", mesg);

}
```

```Ghidra
void f_mess(void)

{
  long in_FS_OFFSET;
  undefined8 local_48;
  undefined8 local_40;
  undefined8 local_38;
  undefined8 local_30;
  undefined8 local_28;
  undefined8 local_20;
  undefined2 local_18;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  local_48 = 0x2073706168726550;
  local_40 = 0x7463657078652049;
  local_38 = 0x756d206f74204465;
  local_30 = 0x6f7920666f206863;
  local_28 = 0x797274202e2e2e75;
  local_20 = 0x2e2e6e6961676120;
  local_18 = 0xa2e;
  printf("%s",&local_48);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
```
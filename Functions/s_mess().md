```source
void s_mess() {

	char mesg[] = {0x79, 0x6F, 0x75, 0x20, 0x64, 0x69, 0x64, 0x20, 0x69, 0x74, 0x21, 0x20, 0x50, 0x72, 0x6F, 0x75, 0x64, 0x2C, 0x20, 0x49, 0x73, 0x20, 0x74, 0x68, 0x65, 0x20, 0x6F, 0x6E, 0x6C, 0x79, 0x20, 0x77, 0x6F, 0x72, 0x44, 0x20, 0x69, 0x20, 0x63, 0x61, 0x6E, 0x20, 0x75, 0x73, 0x65, 0x20, 0x74, 0x6F, 0x20, 0x63, 0x6F, 0x6E, 0x67, 0x72, 0x61, 0x74, 0x75, 0x6C, 0x61, 0x74, 0x65, 0x20, 0x79, 0x6F, 0x75, 0x21, 0x0A};

	printf("%s", mesg);

}
```

```Ghidra
void s_mess(void)

{
  long in_FS_OFFSET;
  undefined8 local_58;
  undefined8 local_50;
  undefined8 local_48;
  undefined8 local_40;
  undefined8 local_38;
  undefined8 local_30;
  undefined8 local_28;
  undefined8 local_20;
  undefined2 local_18;
  undefined1 local_16;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  local_58 = 0x2064696420756f79;
  local_50 = 0x756f725020217469;
  local_48 = 0x6874207349202c64;
  local_40 = 0x7720796c6e6f2065;
  local_38 = 0x616320692044726f;
  local_30 = 0x6f7420657375206e;
  local_28 = 0x746172676e6f6320;
  local_20 = 0x6f79206574616c75;
  local_18 = 0x2175;
  local_16 = 10;
  printf("%s",&local_58);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return;
}
```
gcc processID.c -o processID
```processID.c
#include <stdio.h>
#include <unistd.h>
#include <stdbool.h>

void s_mess();
void f_mess();
void w_mess();
bool compare_two();
int compare();
void print_asts();
int user_input;

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

void s_mess() {
	char mesg[] = {0x79, 0x6F, 0x75, 0x20, 0x64, 0x69, 0x64, 0x20, 0x69, 0x74, 0x21, 0x20, 0x50, 0x72, 0x6F, 0x75, 0x64, 0x2C, 0x20, 0x49, 0x73, 0x20, 0x74, 0x68, 0x65, 0x20, 0x6F, 0x6E, 0x6C, 0x79, 0x20, 0x77, 0x6F, 0x72, 0x44, 0x20, 0x69, 0x20, 0x63, 0x61, 0x6E, 0x20, 0x75, 0x73, 0x65, 0x20, 0x74, 0x6F, 0x20, 0x63, 0x6F, 0x6E, 0x67, 0x72, 0x61, 0x74, 0x75, 0x6C, 0x61, 0x74, 0x65, 0x20, 0x79, 0x6F, 0x75, 0x21, 0x0A};
	printf("%s", mesg);
} 

void f_mess() {
	char mesg[] = {80, 101, 114, 104, 97, 112, 115, 32, 73, 32, 101, 120, 112, 101, 99, 116, 101, 68, 32, 116, 111, 32, 109, 117, 99, 104, 32, 111, 102, 32, 121, 111, 117, 46, 46, 46, 32, 116, 114, 121, 32, 97, 103, 97, 105, 110, 46, 46, 46, 10};
	printf("%s", mesg);
}

int compare(int user_input) {
	if(compare_two && (user_input == getpid())) {
		return 1;
	}
	else {
		return 0;
	}
}

bool compare_two() {
	if(255 & 0) {
		return 0;
	}
	else {
		return 0+1;
	}
}

void w_mess() {
	print_asts(32);
	printf("*****    W E L C O M E    *****\n");
	print_asts(32);
	printf("**    Your task is to find    **\n");
	printf("** the secret, changing, code **\n");
	print_asts(32);
	printf("\nRules:\n1. No brute forcing\n");
}

void print_asts(int n){
	for(int i = 0; i < n; i++) {
		putchar('*');
	}
	printf("\n");
}

/* NOTES:
 * This script is intentionally winding to make reverse engineering/ debugging
 * as difficult as possible, just to test myself/ learn C!
 *
*/
```


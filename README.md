# Become A Millionaire
Please proceed to the `millionaire` folder.

You will also be exploiting the format string vulnerability to get the flag.

Your job is to provide malicious input to the program `launcher`. Here is the source code of this program:

```cpp
void shell(void) {
  setregid(getegid(), getegid());
  system("echo "Your flag is:"; cat flag\n");
}

void process_user_input(void) {
  char buf[16] = {"\0"};
  char str[12] = "You'll get:";

  // get your input
  printf("Your buf address: %p\n", buf);
  printf("Secret message: \"%s $%u\"\n", str, buf[0]);
  printf("Enter the input to print out: ");
  if (fgets(buf, 28, stdin) == NULL)
    return;

  // print out the buffer
  printf(buf);
  printf("Secret message: \"%s $%u\" (exploited)\n", str, buf[0]);

  // print out the flag
  if ((unsigned int) buf[0] > 100000)
    shell();
  else
    printf("No luck; you're not a millionaire...\n");
}

int main(void) { ...... process_user_input(); }
```

Once you run it, the program will wait for your input (that will be used as the argument of printf function). You have two jobs here: (1) find out the memory addresses where the pref and flag are (HINT: you can use `%p %p ..` to inspect where each memory address points to) and (2) use the format string vulnerability with the addresses that you figured out to print the flag. You can take a look at the lecture slides.

If you are successful, you will have the flag.

Good luck.

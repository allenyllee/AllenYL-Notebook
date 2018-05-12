# C_Cpp__語言筆記

## Ref

- [cplusplus.com - The C++ Resources Network](http://www.cplusplus.com/)
- 


## Standard Library

- [What are the C and C++ Standard Libraries? - Internal Pointers](https://www.internalpointers.com/post/c-c-standard-library)

    - [什么是 C 和 C ++ 标准库？ - 技术翻译 - 开源中国社区](https://www.oschina.net/translate/c-c-standard-library?from=20180506)

    some people over the Internet are trying to create [working programs](http://weeb.ddns.net/0/programming/c_without_standard_library_linux.txt) without involving Standard Library. This way you lose portability, because you rely upon functions provided by a specific operating system. However going the hard way may teach you a lot and make you more aware of what you are doing even when using high level libraries.
    
    you don't want to include the Standard Library when working on embedded systems: with limited memory available every byte matters so you tend to write more assembly because the code doesn't need to be portable. 
    
    The [demoscene](https://en.wikipedia.org/wiki/Demoscene) is another setting where people strive to fit beautiful audio-visual presentations into program binaries of limited size — 4K still isn't the lowest border: some demoparties organize 1K, 256 byte, 64 byte or even 32 byte intro competitions. No Standard Library allowed in there!
    

## C

### C function pointer

- [c - How can I use an array of function pointers? - Stack Overflow](https://stackoverflow.com/questions/252748/how-can-i-use-an-array-of-function-pointers)

    > ```c
    > typedef int FUNC(int, int);
    > 
    > FUNC sum, subtract, mul, div;
    > FUNC *p[4] = { sum, subtract, mul, div };
    > 
    > int main(void)
    > {
    >     int result;
    >     int i = 2, j = 3, op = 2;  // 2: mul
    > 
    >     result = p[op](i, j);   // = 6
    > }
    > 
    > // maybe even in another file
    > int sum(int a, int b) { return a+b; }
    > int subtract(int a, int b) { return a-b; }
    > int mul(int a, int b) { return a*b; }
    > int div(int a, int b) { return a/b; }
    > 
    > ```
    > 

### C array initialize

- [c - How to initialize only few elements of an array with some values? - Stack Overflow](https://stackoverflow.com/questions/38860046/how-to-initialize-only-few-elements-of-an-array-with-some-values)

    > In C, Yes. Use designated initializer (added in C99 and not supported in C++).
    > 
    > ```c
    > int array[12] = {[0] = 1, [4] = 2, [8] = 3};
    > ```
    > 


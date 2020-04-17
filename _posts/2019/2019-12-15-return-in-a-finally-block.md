---
date: 2019/12/15 08:15
categories:
- java
title: Return in a finally block

---
What will happen if we return a value in a finally block?

If the finally block executes successfully the return in the finally block will override the return value set in the try-catch block.

    package org.magicworldz.basic.finallyreturn;
    
    public class FinallyReturn {
        public static void main(String[] args) {
            var app = new FinallyReturn();
            System.out.println(app.finallyReturn(5));
        }
    
        public int finallyReturn(int ret) {
            try {
                return ret;
            } finally {
                return 0;
            }
        }
    
    }

Call the `finallyReturn(2)` will get `0`.

The finally block will execute no matter exception handled or not. But in some special cases, the finally block will not been executed.

1. When an exception occurs in the first line of the finally block. It will execute if an exception occurs in other lines.
2. `System.exit(int)` is invoked.
3. The thread dies
4. Close the CPU
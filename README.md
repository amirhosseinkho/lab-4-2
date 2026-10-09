> Persian version: [README.fa.md](README.fa.md)

# lab-4-2: Profiling and optimizing Java code

## Part 1: Finding and fixing a performance problem with a profiler

After installing and starting the profiler, we connect it to the IDE (IntelliJ IDEA):

![Screenshot 2024-08-06 184232](https://github.com/user-attachments/assets/ab8125e0-423c-4ca1-b5d5-ccb8a8f3a2c0)
![Screenshot 2024-08-06 184410](https://github.com/user-attachments/assets/ca2ce6da-73c0-4333-9b02-dca353f5f9af)

We then run it on the target class and examine the class's methods together with their CPU and memory use:

![Screenshot 2024-08-06 184543](https://github.com/user-attachments/assets/1a40bf74-3884-4868-a0a2-846b74561bfc)

As the next screenshot shows, the program ran without problems. With a somewhat larger loop, however, it would take much more time and memory. Below we increase the loop size and see the program run into trouble:

![Screenshot 2024-08-06 184749](https://github.com/user-attachments/assets/8e262fbf-48e5-4fc3-b827-feb2812f868c)
![Screenshot 2024-08-06 184647](https://github.com/user-attachments/assets/4ad973d6-c1db-464e-9537-638d9b81157f)
![Screenshot 2024-08-06 184900](https://github.com/user-attachments/assets/c3d4b10a-b286-4d7e-89a7-8bfbab477c00)
![Screenshot 2024-08-06 184917](https://github.com/user-attachments/assets/b54beaf8-f527-4e10-acc9-0fdf12999646)

The program failed with an error, and its CPU and memory use rose well above normal. Next we look for the part of the code that causes this. As the screenshots below show, most of the CPU time was spent in `temp()`.

![Screenshot 2024-08-06 185121](https://github.com/user-attachments/assets/1794826b-61e9-4b7c-aec1-3c01583b7cfd)
![Screenshot 2024-08-06 185215](https://github.com/user-attachments/assets/184ca333-82e6-4a06-86fd-3d10ce6f5b21)
![Screenshot 2024-08-06 185244](https://github.com/user-attachments/assets/73a511a5-d2b8-4806-b04d-1e5728fe81ec)

To fix the code, we replace the `ArrayList` with fixed-size arrays, because an `ArrayList` uses more memory and is slower to process. As the screenshot below shows, each loop iteration now uses an array of fixed size. Profiling the program again shows its resource use; the code now runs without errors and faster:

![after](https://github.com/user-attachments/assets/2e2be2b2-7b92-4fbd-942d-e22a9966fe84)
![Screenshot 2024-08-06 185836](https://github.com/user-attachments/assets/d290d618-65e7-4c4b-af59-f86d77a04a7b)
![after 2](https://github.com/user-attachments/assets/8028519c-8a6a-4d96-886d-4b513f2e329c)
![after 3](https://github.com/user-attachments/assets/fb21bcef-a75d-438d-b184-e053cef7ff53)

After the fix, resource use is much lower and `temp()` runs faster. This shows how much choosing the right algorithm can improve a program's performance.

## Part 2: Optimizing a recursive algorithm

Algorithms that use recursion can consume a lot of resources. A well-known example is counting the possible paths in an M×N grid, which becomes very expensive without optimization.

We first write a simple recursive program that counts the possible paths in an M×N grid, and then optimize it to reduce its resource use.

![1](https://github.com/user-attachments/assets/a7b1b0fa-812f-405b-8f6c-4db64fda04cd)

![Screenshot 2024-08-06 194901](https://github.com/user-attachments/assets/59c2e1e2-6f06-4e21-9290-23ce8be79bf8)
![Screenshot 2024-08-06 194918](https://github.com/user-attachments/assets/9e540bf4-4d6a-48cc-8d88-7361b145491f)
![Screenshot 2024-08-06 194939](https://github.com/user-attachments/assets/adeb3dbf-7fda-4f52-87b4-502228262052)

The original code uses plain recursion, which repeats many calculations and therefore uses a lot of resources. The optimized code stores the number of possible paths for each grid cell in a two-dimensional array (`dp`). This removes the repeated calculations and lowers resource use.

![Screenshot 2024-08-06 195227](https://github.com/user-attachments/assets/fb4e42de-b475-4158-8650-ddc1972b78fe)
![Screenshot 2024-08-06 195307](https://github.com/user-attachments/assets/cb858586-397b-44cc-8b6e-b7dbe9038c55)

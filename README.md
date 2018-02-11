# Here is HarekazeCTF-2018-problem that I authored.

### What is HarekazeCTF2018?

[HarekazeCTF2018](https://harekaze.com/ctf.html)

[CTFtime.org](https://ctftime.org/event/549)


---

## Problem Name: Lost_data

- Problem file: [lost_data.zip](https://github.com/hiww/HarekazeCTF-2018/blob/master/lost_data.zip)
    
    - Points 100, Genre For + Misc, Author hiww, Solves 54.

```
Description
Guess or try xxxxx in flag and replace to the correct word.
xxxxx is uppercase.
No need decipher the password of xxxxx.zip.
lost_data.zip
Hint:
Refer the file contents of xxxxx.zip.
filesystem is answer.
(For + Misc, 100 points)
```


## Solution(Writeup):

- Step-1.(Recover QR-code from data.zip)
    - Unzip the data.zip.
        - 1. The first 4 bytes of each file is `89 2E 2E 2E`.
        - 2. Even if using the file command the extension is unknown.
        - 3. But, there are some hint in the files[1..3].
        - 4. For example, `49 44 41 54` in hex and `IDAT` in ascii.
        - 5. Replace the first 4 bytes to `89 50 4E 47`. 
        - 6. The lost data was PNG.
        - 7. Scan QR-code by QR-code-scanner(e.g. zbarimg, iOScamera and human).
            
    `QR-code: HarekazeCTF{Y0u_G0t_FuNNy_F1ag_?DF?_T?_is_xxxxx}`
    
- Step-2.(Investigate the xxxxx.zip)
    - By the way, have you ever used SD cards that can not add new files? 
    
    - The filesystem have some restrictions.
        
    - You can know some information by unzip the xxxxx.zip(without password).
        - 1. The contents of xxxxx.zip seems to be fatxxx(file-size is 0KB).
        - 2. Total file number(`512`) means filesystem's number of files limit.
        - 3. Total number of files = Number of files limit in root directory of FAT16.
        - 4. This is why that `FAT16` is correct answer of xxxxx.

- Answer(FLAG):

    - `HarekazeCTF{Y0u_G0t_FuNNy_F1ag_?DF?_T?_is_FAT16}`

- Addition:
    - You can check your filesystem using `df -T`.
    
    - The character string of QR-code was every 16 characters. 


Reference: https://support.microsoft.com/help/436213.

---

# mid test review  
以下是第1大題的5題是非題解釋，根據你的答案（F T T F T），我們來一題一題說明為什麼正確與否：
![image](https://github.com/user-attachments/assets/94f2d19c-eac2-4023-b292-3cf6e08d2d57)


---

### (a) ❌ **F**  
**題目：** In OS terminology, a trap is a hardware instruction that lowers the privilege level from kernel mode to user mode.  
**解析：**  
這題錯的原因是**trap** 是一種**從使用者模式切換到核心模式（user → kernel）**的控制流程，通常是由使用者程式呼叫系統呼叫（system call）來觸發。而從**核心模式回到使用者模式**不是透過 trap，而是由 OS 完成任務後透過某種機制回到 user mode。因此敘述錯誤。

---

### (b) ✅ **T**  
**題目：** When the OS performs a context switch from process A to process B, the OS would save its kernel register values into the PCB of process A.  
**解析：**  
沒錯。當進行 context switch 時，OS 會儲存當前執行緒（process A）的狀態（registers、program counter、stack pointer 等）到 A 的 PCB（Process Control Block）裡，以便將來可以恢復它的狀態。這樣才能順利地切換到 process B。

---

### (c) ✅ **T**  
**題目：** When we print out the address of a variable in our user program, the printed address is a virtual address.  
**解析：**  
對的。使用者程式存取的都是虛擬位址（virtual address），真實的記憶體位址（physical address）是由 OS 透過記憶體管理單元（MMU）來做轉換。因此 `&var` 這樣印出來的是虛擬位址。

---

### (d) ❌ **F**  
**題目：** A page fault occurs if the OS cannot perform address translation from the TLB.  
**解析：**  
這題錯在過度簡化。**TLB miss ≠ Page fault**。  
TLB（Translation Lookaside Buffer）只是一個快取，如果 miss，OS 還可以從頁表（page table）找到對應的 physical frame。如果連頁表都找不到該頁，**才會發生 page fault**。所以這題敘述錯誤。

---

### (e) ✅ **T**  
**題目：** In a multi-level feedback queue, a job may suffer from starvation if the scheduler do not bring it back to the topmost queue.  
**解析：**  
正確。**Multi-level feedback queue（MLFQ）** 是一種根據行為動態調整優先級的排程方式。如果 scheduler 沒有設計機制讓低優先級的 job 有機會被提升（例如經過一段時間沒執行就回到高優先級隊列），那麼這些 job 就有可能被一直餓著（starvation）。

---

![image](https://github.com/user-attachments/assets/7b79180e-ba5b-456f-b4e5-b65fe20037c4)

好，我來幫你逐步解析第2題，並解釋為什麼在 **t = 0, 2, 3, 4, 6, 7, 9** 時會發生 **page fault**。

---

## ✅ 題目重點整理：
- 有 **4 個 virtual pages**（編號 0,1,2,3）  
- 有 **3 個實體 frames（空的）**  
- 使用 **LRU（Least Recently Used）** 頁面替換政策  
- 虛擬頁面存取順序為：
```
1 (t=0), 1, 2, 0, 3, 2, 1, 0, 1, 3 (t=9)
```

---

### 🔁 Step by Step 模擬 + 解釋：
初始化：3 個實體 frame 是空的

---

#### 🕒 t = 0 → access VPN 1  
- 在實體記憶體中找不到 → Page fault ✅  
- 將 1 放進記憶體 → Memory: [1]  

---

#### 🕒 t = 1 → access VPN 1  
- 已經在記憶體 → ✅ No page fault  
- 更新 LRU：1 最近使用

---

#### 🕒 t = 2 → access VPN 2  
- 找不到 → Page fault ✅  
- 加進記憶體 → Memory: [1, 2]  

---

#### 🕒 t = 3 → access VPN 0  
- 找不到 → Page fault ✅  
- 加進記憶體 → Memory: [1, 2, 0]（已滿）  

---

#### 🕒 t = 4 → access VPN 3  
- 找不到 → Page fault ✅  
- 記憶體已滿，用 **LRU** 替換  
- LRU 判斷：最久沒用的是 VPN 1（t=1 用過）  
- 替換 1 → Memory: [3, 2, 0]

---

#### 🕒 t = 5 → access VPN 2  
- 已經在記憶體 → No page fault ✅  
- 更新 LRU：2 最近使用

---

#### 🕒 t = 6 → access VPN 1  
- 找不到 → Page fault ✅  
- 替換：目前在記憶體的是 [3, 2, 0]  
- 最近沒用的是 0（t=3 使用過）  
- 替換 0 → Memory: [3, 2, 1]  

---

#### 🕒 t = 7 → access VPN 0  
- 找不到 → Page fault ✅  
- 替換：最久沒用的是 3（t=4 用過）  
- 替換 3 → Memory: [0, 2, 1]

---

#### 🕒 t = 8 → access VPN 1  
- 已在記憶體中 → No page fault ✅  
- 更新 LRU：1 最近使用

---

#### 🕒 t = 9 → access VPN 3  
- 找不到 → Page fault ✅  
- 替換：最久沒用的是 2（t=5 用過）  
- 替換 2 → Memory: [0, 3, 1]

---

## ✅ Page Fault 發生時間點：
```
t = 0, 2, 3, 4, 6, 7, 9 （共7次）
```
![image](https://github.com/user-attachments/assets/c69abc15-e919-4dcc-9c12-b79073390e9c)



  ![image](https://github.com/user-attachments/assets/83f9a7f6-f993-4273-8c22-7e78408a923b)


  ![image](https://github.com/user-attachments/assets/e59ffc19-35c2-4b25-a6a0-4c7015d3b2cf)

  First-fit : 第一個找到空間夠大的就放進去  
Best-fit : 只找到大小剛好的或者最小卻剛好夠的，但可能會有壞處就是造成了剩下一點小小的別人也無法使用  
Worst-fit : 找空間最大的記憶體區段來放入  
https://ithelp.ithome.com.tw/articles/10226191  

![image](https://github.com/user-attachments/assets/aeecc54f-59da-4a5d-9287-194ef751525e)

![image](https://github.com/user-attachments/assets/6afe4c70-4110-483d-ae65-699dcc0eb117)

![image](https://github.com/user-attachments/assets/dfff3c0b-424f-44ed-9fc5-e9422966cad1)  

![image](https://github.com/user-attachments/assets/d642aae2-d0eb-4b99-a5c1-50687db22ba3)


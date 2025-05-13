# OS
用來學習作業系統(OSTEP)的筆記和程式碼

周次|日期(一；五)  
w 1|2/17；2/21  
W 2|2/24；  
W 3|3/ 3；3/ 7  
W 4|3/10；3/14  
W 5|3/17；3/21  
W 6|3/24；3/28  
W 7|3/31；  
W 8|mid test：4/7；4/11 fri.(async)  
  
W 9|4/14；4/18  
W10|4/21；4/25  
W11|4/28；5/ 2  
W12|5/ 5；5/ 9  
W13|5/12；5/16  
W14|5/19；5/23  
W15|5/26(講座)；5/30  
W16|final：6/2；6/6  


4/14  
- introduction to concumency
- motivation
- challenge
- opitimization
- implementation
keyword
- thread
- PC(program counter)in x86 call rip
- Pthread(POSIX)
- rip-relative addressing(PIC = position-independent-code)
- non-deterministic execution
- critical section = block of code can shared
- race condition
- mutual exclusion 互斥mutex
- guard
- test-and-set
- atomicity
4/25
- semaphores(號誌)  
  applications(應用)  
  1.atomic execution(原子操作)
    - atomic execution 是指利用初始值為 1 的 semaphore 保護 critical section，透過 sem_wait() 取得資源、sem_post() 釋放資源，保證同一時間只有一個 thread 能進入該區域，達成互斥控制。
    - 說明它是保護 critical section 的互斥操作，sem_wait/sem_post 本身是 atomic  
  2.event ordering(事件排序)
    - event ordering 是指透過初始值為 0 的 semaphore，在 thread A 執行 sem_post()，再讓 thread B 執行 sem_wait()，來保證 A 的某個事件（例如初始化資源）發生在 B 的動作（如使用資源）之前。這樣就建立了 A 在 B 之前的事件順序。  
  3.producer/consumer(生產者/消費者)  
    若一個 thread 先取得某個 lock，另一個 thread 則無法繼續執行，雙方互相等待對方釋放資源，導致永遠無法前進，這就是死鎖（deadlock）的情況。  
    或者更精簡一點：  
    當兩個 thread 各自持有一部分資源，並且等待對方釋放另一部分資源，雙方互相等待而永遠無法繼續，這種情況稱為死鎖。  
- concurrency Bugs
  - deadlock bug
  - non-deadlock bugs  
  
4/28  
- concurrency Bugs
  - deadlock bug  
    這塊沒什麼問題，理解4個條件，若P則Q；非Q則非P的關係，以及在consumer/producer的情境4條件的意義。  
  - non-deadlock bugs
    - atomicity violation
      參考https://hackmd.io/@sysprog/concurrency-atomics  
    - order violation  
      這兩個還待理解。  
- semaphore types
  - unnamed semaphores(memory-based)
  - named semaphores(file-based)  
  33:00 如果是2個process之間的thread要synchronize，但semaphore存在P1的heap裡面，那會有問題。這時就會用到不同types的semaphore。(待確認  
- I/O devices
  - memory-mapped I/O
  - explicit I/O instructions

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
  2.event ordering(事件排序)  
  3.producer/consumer(生產者/消費者)  
    若一個 thread 先取得某個 lock，另一個 thread 則無法繼續執行，雙方互相等待對方釋放資源，導致永遠無法前進，這就是死鎖（deadlock）的情況。  
    或者更精簡一點：  
    當兩個 thread 各自持有一部分資源，並且等待對方釋放另一部分資源，雙方互相等待而永遠無法繼續，這種情況稱為死鎖。  
- concurrency Bugs
- deadlock bug
- non-deadlock bugs


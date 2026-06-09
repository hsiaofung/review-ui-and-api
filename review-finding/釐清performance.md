<!-- 粗略算出 performance -->
Performance issue 的算法:

例如: 
const categories = list.map(x => x.category)

1. 實際 CPU 做的事

    對每一筆：
    - 讀 memory
    - string compare / copy
    - push 到 array

    👉 約略可以當成： ~10 ~ 50 CPU instructions / item（很粗略估）

2. 粗略算一次 cost
    - 我們用保守估計：3000 items × 30 instructions = 90,000 instructions

3. 換成 CPU 時間
    - 現代 CPU：約 3GHz = 3,000,000,000 cycles / sec
    - 假設：1 instruction ≈ 1~3 cycles
    - 👉 粗估： 90,000 instructions ≈ 270,000 cycles (保守)

4. 換算時間：
    - 270,000 / 3,000,000,000 = 0.00009 seconds = 0.09 ms

5. 現實 browser overhead
    但實務上要加：
    - JS engine overhead
    - object allocation
    - GC pressure
    - framework overhead
    - 👉 放大 10~50 倍（很保守）
    - 👉 final estimate： ~1ms ~ 5ms
    - 結論: A 3000-item O(n) operation in frontend typically costs ~1–5ms.

6. 跟真正 expensive 的東西比
    - DOM render（1 row）: ~0.2 ~ 2ms
        - 3000 rows table：可能 100ms ~ 500ms（甚至更多）
    - API request(network latency)：50ms ~ 300ms+
      Network RTT          20ms
      Backend Process      30ms
      JSON Transfer         5ms
      -------------------------
      Total                55ms  

      - RTT(Round Trip Time): 往返時間。一個封包從瀏覽器送到伺服器，再從伺服器回到瀏覽器所花的時間。
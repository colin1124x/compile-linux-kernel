- Periodictimer ticks (constant rate, no dynticks)
    - 無論CPU是否需要,都強制按照固定頻率不斷觸發時鐘中斷.這是最耗電的方式,不推薦使用
- Idle dynticks system (tickless idle)
    - CPU在空閒狀態時不產生不必要的時鐘中斷,以使處理器能夠在較低能耗狀態下運行以節約電力
- Full dynticks system (tickless)
    - 即使CPU在忙碌狀態也盡可能關閉所有時鐘中斷,適用於CPU在同一時間僅運行一個任務,或者用戶空間程序極少與內核交互的場合
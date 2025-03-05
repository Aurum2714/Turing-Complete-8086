# 日誌
===
## D1
---
  先將整個工作流程分各個階段已完成階段性目標為主
### ALU
#### 算術運算（Arithmetic Operations）
    ADD    加法運算（A = A + B）	        CF, PF, AF, ZF, SF, OF
    ADC    帶進位加法（A = A + B + CF）	CF, PF, AF, ZF, SF, OF
    SUB    減法運算（A = A - B）	        CF, PF, AF, ZF, SF, OF
    SBB    帶借位減法（A = A - B - CF）	CF, PF, AF, ZF, SF, OF
    MUL    無符號乘法（A = A * B）	      CF, OF
    IMUL   有符號乘法（A = A * B）	      CF, OF
    DIV    無符號除法（A ÷ B）	          除 0 例外
    IDIV   有符號除法（A ÷ B）	          除 0 例外
    INC    遞增（A = A + 1）	            PF, AF, ZF, SF, OF
    DEC    遞減（A = A - 1）	            PF, AF, ZF, SF, OF
    NEG    取反（A = -A，即補數運算）	    CF, PF, AF, ZF, SF, OF
#### 邏輯運算（Logical Operations）
    AND	 位元 AND（A = A & B）	PF, ZF, SF
    OR	 位元 OR（A = A | B）	PF, ZF, SF
    XOR	 位元 XOR（A = A ⊕ B）	PF, ZF, SF
    NOT	 取反（A = ~A）	無影響
#### 比較運算（Comparison Operations）
    CMP	比較（A - B，但不存結果）	CF, PF, AF, ZF, SF, OF
    TEST	測試（A & B，但不存結果）	PF, ZF, SF
#### 位元操作（Bitwise Operations）
    SHL	左移（A << n，低位補 0）	CF, PF, ZF, SF, OF
    SAL	算術左移（同 SHL）	CF, PF, ZF, SF, OF
    SHR	無符號右移（A >> n，高位補 0）	CF, PF, ZF, SF, OF
    SAR	算術右移（A >> n，高位補符號位）	CF, PF, ZF, SF, OF
    ROL	循環左移（A 左移，最高位進 CF，再進最低位）	CF
    ROR	循環右移（A 右移，最低位進 CF，再進最高位）	CF
    RCL	透過 CF 進行左移（CF 參與運算）	CF
    RCR	透過 CF 進行右移（CF 參與運算）	CF
#### 狀態標誌更新（FLAGS Register Updates）
    CF（Carry Flag）	進位/借位標誌	ADD, SUB, SHL, SHR
    ZF（Zero Flag）	結果為 0	ADD, SUB, AND, CMP
    SF（Sign Flag）	符號（最高位 1 為負數）	ADD, SUB, CMP
    OF（Overflow Flag）	溢位	ADD, SUB, IMUL
    PF（Parity Flag）	結果的低 8 位內 1 的數量為偶數	ADD, SUB, XOR, AND
    AF（Auxiliary Carry）	BCD 計算進位（用於十進制運算）	ADD, SUB, ADC
### 如何透過 Opcode 判斷 ALU
    ADD	000000dw	加法（Adder）
    SUB	001010dw	減法（Adder）
    CMP	001110dw	比較（Adder）
    AND	001000dw	位元 AND（Logical Unit）
    OR	000010dw	位元 OR（Logical Unit）
    XOR	001100dw	位元 XOR（Logical Unit）
    NOT	1111011w	位元 NOT（Logical Unit）
    SHL	1101000w	左移（Shifter）
    SHR	1101001w	右移（Shifter）
    MUL	1111011w	無符號乘法（Multiplier）
    IMUL	1111011w	有符號乘法（Multiplier）
    DIV	1111011w	無符號除法（Divider）
    IDIV	1111011w	有符號除法（Divider）
d（方向位元）：0 = 來源 -> 目的，1 = 目的 -> 來源
w（運算寬度）：0 = 8-bit，1 = 16-bit

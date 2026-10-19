# SMD Resistor Codes
> **ELECTRICAL CHEAT SHEET** &nbsp;|&nbsp; *Decoder for surface-mount resistor markings — 3-digit (E24, 5%), 4-digit (E96, 1%), and EIA-96 (1% precision) per IEC 60062.*

---

## <span style="color: #0056b3;">How the Three Systems Work</span>

| SYSTEM | FORMAT | DECODING | TYPICAL TOLERANCE | EXAMPLE |
| :--- | :---: | :--- | :--- | :--- |
| **3-digit** | `ABC` | $AB \times 10^C\ \Omega$ | ±5% (E24 series) | $472 = 47 \times 10^2 = 4.7\ \text{k}\Omega$ |
| **4-digit** | `ABCD` | $ABC \times 10^D\ \Omega$ | ±1% (E96 series) | $4992 = 499 \times 10^2 = 49.9\ \text{k}\Omega$ |
| **EIA-96** | `NNX` | (base from table for `NN`) $\times$ (multiplier from table for `X`) | ±1% (E96 series) | $01C = 100 \times 100 = 10\ \text{k}\Omega$ |
| **"R" notation** | e.g. `4R7`, `R47`, `0R10` | `R` = decimal point | Varies *(read marking direction carefully)* | $4\text{R}7 = 4.7\ \Omega;\ \text{R}47 = 0.47\ \Omega;\ 0\text{R}10 = 0.10\ \Omega$ |
| **Zero-ohm jumper** | `0`, `00`, `000`, `0000` | Not a resistor; wire bridge | N/A | Used to route traces without a via |

> [!TIP]
> **Quick rule of thumb:** Count digits and check for letters.
> - **Three numbers** = General purpose (5%)
> - **Four numbers** = Precision (1%)
> - **Two numbers + letter** = EIA-96 (1%, compact)

---

## <span style="color: #0056b3;">Reading 3-Digit Codes</span>

The first two digits are the significant figures; the third is the multiplier (power of 10).

| MARKING | CALCULATION | VALUE |
| :---: | :---: | :---: |
| `100` | $10 \times 10^0$ | $10\ \Omega$ |
| `220` | $22 \times 10^0$ | $22\ \Omega$ |
| `470` | $47 \times 10^0$ | $47\ \Omega$ |
| `101` | $10 \times 10^1$ | $100\ \Omega$ |
| `221` | $22 \times 10^1$ | $220\ \Omega$ |
| `472` | $47 \times 10^2$ | $4.7\ \text{k}\Omega$ |
| `103` | $10 \times 10^3$ | $10\ \text{k}\Omega$ |
| `104` | $10 \times 10^4$ | $100\ \text{k}\Omega$ |
| `105` | $10 \times 10^5$ | $1\ \text{M}\Omega$ |
| `106` | $10 \times 10^6$ | $10\ \text{M}\Omega$ |

> [!WARNING]
> **Watch out:** `100` means $10\ \Omega$ ($10 \times 10^0$), **not** $100\ \Omega$. The trailing zero is the multiplier, not the third significant digit. For $100\ \Omega$, the code is `101`.

---

## <span style="color: #0056b3;">Reading 4-Digit Codes (Precision)</span>

First three digits are significant figures; fourth is the multiplier. Used for $\pm 1\%$ E96 series.

| MARKING | CALCULATION | VALUE |
| :---: | :---: | :---: |
| `1000` | $100 \times 10^0$ | $100\ \Omega$ |
| `4700` | $470 \times 10^0$ | $470\ \Omega$ |
| `1001` | $100 \times 10^1$ | $1\ \text{k}\Omega$ |
| `4991` | $499 \times 10^1$ | $4.99\ \text{k}\Omega$ |
| `1002` | $100 \times 10^2$ | $10\ \text{k}\Omega$ |
| `4992` | $499 \times 10^2$ | $49.9\ \text{k}\Omega$ |
| `1003` | $100 \times 10^3$ | $100\ \text{k}\Omega$ |
| `1004` | $100 \times 10^4$ | $1\ \text{M}\Omega$ |

---

## <span style="color: #0056b3;">EIA-96 Multiplier Letters</span>

The third character of an EIA-96 code is a letter giving the multiplier:

| LETTER | MULTIPLIER | LETTER | MULTIPLIER |
| :---: | :---: | :---: | :---: |
| **Z** | $\times 0.001$ | **D** | $\times 1000$ |
| **Y** or **R** | $\times 0.01$ | **E** | $\times 10000$ |
| **X** or **S** | $\times 0.1$ | **F** | $\times 100000$ |
| **A** | $\times 1$ | — | — |
| **B** or **H** | $\times 10$ | — | — |
| **C** | $\times 100$ | — | — |

> [!NOTE]
> In practice, **A, B, C, X** cover 99% of what you'll see. The duplicates (`Y/R`, `X/S`, `B/H`) come from harmonizing different national standards.

---

## <span style="color: #0056b3;">EIA-96 Base Value Table (Codes 01–96)</span>

The first two digits of an EIA-96 marking look up a base value in this table (E96 series, $\pm 1\%$ standard values):

| CODE | VALUE | CODE | VALUE | CODE | VALUE | CODE | VALUE |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **01** | 100 | **25** | 178 | **49** | 316 | **73** | 562 |
| **02** | 102 | **26** | 182 | **50** | 324 | **74** | 576 |
| **03** | 105 | **27** | 187 | **51** | 332 | **75** | 590 |
| **04** | 107 | **28** | 191 | **52** | 340 | **76** | 604 |
| **05** | 110 | **29** | 196 | **53** | 348 | **77** | 619 |
| **06** | 113 | **30** | 200 | **54** | 357 | **78** | 634 |
| **07** | 115 | **31** | 205 | **55** | 365 | **79** | 649 |
| **08** | 118 | **32** | 210 | **56** | 374 | **80** | 665 |
| **09** | 121 | **33** | 215 | **57** | 383 | **81** | 681 |
| **10** | 124 | **34** | 221 | **58** | 392 | **82** | 698 |
| **11** | 127 | **35** | 226 | **59** | 402 | **83** | 715 |
| **12** | 130 | **36** | 232 | **60** | 412 | **84** | 732 |
| **13** | 133 | **37** | 237 | **61** | 422 | **85** | 750 |
| **14** | 137 | **38** | 243 | **62** | 432 | **86** | 768 |
| **15** | 140 | **39** | 249 | **63** | 442 | **87** | 787 |
| **16** | 143 | **40** | 255 | **64** | 453 | **88** | 806 |
| **17** | 147 | **41** | 261 | **65** | 464 | **89** | 825 |
| **18** | 150 | **42** | 267 | **66** | 475 | **90** | 845 |
| **19** | 154 | **43** | 274 | **67** | 487 | **91** | 866 |
| **20** | 158 | **44** | 280 | **68** | 499 | **92** | 887 |
| **21** | 162 | **45** | 287 | **69** | 511 | **93** | 909 |
| **22** | 165 | **46** | 294 | **70** | 523 | **94** | 931 |
| **23** | 169 | **47** | 301 | **71** | 536 | **95** | 953 |
| **24** | 174 | **48** | 309 | **72** | 549 | **96** | 976 |

---

### Worked EIA-96 Examples

| MARKING | BASE (FROM TABLE) | MULTIPLIER (FROM LETTER) | VALUE |
| :---: | :---: | :---: | :---: |
| `01A` | 01 $\rightarrow$ 100 | A $\rightarrow \times 1$ | $100\ \Omega$ |
| `01B` | 01 $\rightarrow$ 100 | B $\rightarrow \times 10$ | $1\ \text{k}\Omega$ |
| `01C` | 01 $\rightarrow$ 100 | C $\rightarrow \times 100$ | $10\ \text{k}\Omega$ |
| `29B` | 29 $\rightarrow$ 196 | B $\rightarrow \times 10$ | $1.96\ \text{k}\Omega$ |
| `38C` | 38 $\rightarrow$ 243 | C $\rightarrow \times 100$ | $24.3\ \text{k}\Omega$ |
| `39D` | 39 $\rightarrow$ 249 | D $\rightarrow \times 1000$ | $249\ \text{k}\Omega$ |
| `68X` | 68 $\rightarrow$ 499 | X $\rightarrow \times 0.1$ | $49.9\ \Omega$ |
| `92Z` | 92 $\rightarrow$ 887 | Z $\rightarrow \times 0.001$ | $0.887\ \Omega$ |

---

## <span style="color: #0056b3;">Quick Reference: Common Values</span>

| RESISTANCE | 3-DIGIT (5%) | 4-DIGIT (1%) | EIA-96 (1%) |
| :--- | :---: | :---: | :---: |
| **$10\ \Omega$** | `100` | `10R0` | `01X` |
| **$100\ \Omega$** | `101` | `1000` | `01A` |
| **$220\ \Omega$** | `221` | `2200` | `34A` |
| **$330\ \Omega$** | `331` | `3300` | `51A` |
| **$470\ \Omega$** | `471` | `4700` | `66A` |
| **$1\ \text{k}\Omega$** | `102` | `1001` | `01B` |
| **$2.2\ \text{k}\Omega$** | `222` | `2201` | `34B` |
| **$4.7\ \text{k}\Omega$** | `472` | `4701` | `66B` |
| **$10\ \text{k}\Omega$** | `103` | `1002` | `01C` |
| **$22\ \text{k}\Omega$** | `223` | `2202` | `34C` |
| **$47\ \text{k}\Omega$** | `473` | `4702` | `66C` |
| **$100\ \text{k}\Omega$** | `104` | `1003` | `01D` |
| **$1\ \text{M}\Omega$** | `105` | `1004` | `01E` |

---

## <span style="color: #0056b3;">Package Sizes and Typical Markings</span>

| PACKAGE (IMPERIAL) | SIZE (MM) | POWER (W) | TYPICAL MARKING |
| :---: | :---: | :---: | :--- |
| **2512** | $6.4 \times 3.2$ | 1.00 W | 3 or 4 digit |
| **2010** | $5.0 \times 2.5$ | 0.75 W | 3 or 4 digit |
| **1206** | $3.2 \times 1.6$ | 0.25 W | 3 or 4 digit |
| **0805** | $2.0 \times 1.25$ | 0.125 W | 3 or 4 digit |
| **0603** | $1.6 \times 0.8$ | 0.10 W | 3 digit or EIA-96 |
| **0402** | $1.0 \times 0.5$ | 0.063 W | Often unmarked or EIA-96 |
| **0201** | $0.6 \times 0.3$ | 0.05 W | Unmarked (refer to BOM) |
| **01005** | $0.4 \times 0.2$ | 0.031 W | Unmarked (refer to BOM) |

---

## <span style="color: #0056b3;">Common Pitfalls</span>

- **$100 \neq 100\ \Omega$:** In the 3-digit system, `100` is $10 \times 10^0 = 10\ \Omega$. The 3rd digit is the multiplier. For $100\ \Omega$, the marking is `101`.
- **3-digit and 4-digit codes look similar:** A part marked `1001` on an 0805 (4-digit, $1\ \text{k}\Omega$) and `101` on an 0603 (3-digit, $100\ \Omega$) can be easily confused if you don't count digits. **When in doubt, measure.**
- **Underlined codes are precision E24:** In some manufacturer schemes, a `122` (underlined middle digit) or a single underbar indicates precision ($\pm 1\%$ or better) at an E24 value not normally in the precision series.
- **Zero-ohm jumper markings vary:** Single `0`, `00`, `000`, or `0000` all indicate a wire bridge, not a $\Omega$ calculation. Don't try to decode them.
- **Tolerance and tempco aren't on the marking:** The code gives resistance only. For 1%, 0.1%, 0.01% variants or low-tempco precision parts, consult the manufacturer's reel label or BOM.
- **Power rating is in the package, not the code:** An 0603 part marked `103` ($10\ \text{k}\Omega$) is rated for ~0.1 W, while a 1206 with the same `103` marking is rated for 0.25 W. Same value, very different power handling.
- **0402 and smaller usually have no marking:** Below 0603, there is typically no room to print legible characters. Identify parts using the assembly BOM, reel label, or a multimeter.
- **"R" on a non-EIA-96 code means decimal point:** $4\text{R}7 = 4.7\ \Omega$, $\text{R}47 = 0.47\ \Omega$. In EIA-96, `R` is also a multiplier letter ($\times 0.01$). Context determines which: if the code is exactly 3 characters with two digits and one letter at the end, it's EIA-96; otherwise `R` is a decimal point.

---

## <span style="color: #0056b3;">Frequently Asked Questions (FAQ)</span>

### How do I read an SMD marked '472'?
It's a **3-digit code**: the first two digits (`47`) are significant figures, and the third (`2`) is the power-of-10 multiplier.
$$472 = 47 \times 10^2 = 4,700\ \Omega = 4.7\ \text{k}\Omega$$

### What if the resistor has 4 digits like '4701'?
That's the **4-digit precision code** (typically $\pm 1\%$ E96 series). First three digits (`470`) are significant; the fourth (`1`) is the multiplier.
$$4701 = 470 \times 10^1 = 4,700\ \Omega = 4.7\ \text{k}\Omega$$
*(Same value as '472', but $\pm 1\%$ tolerance instead of $\pm 5\%$.)*

### Why does my SMD resistor say '01C' instead of digits?
It's an **EIA-96 code**, used on tiny precision resistors where 4 digits won't fit. First two digits (`01`) look up a base value in the EIA-96 table ($01 = 100$). The letter (`C`) is the multiplier ($C = 100$).
$$01\text{C} = 100 \times 100 = 10,000\ \Omega = 10\ \text{k}\Omega$$

### Why is my SMD resistor blank / no markings?
Below the **0603** ($1.6 \times 0.8\text{ mm}$) package size, there is typically no room for legible markings. **0402** and **0201** resistors often ship unmarked. Identify them via PCB assembly drawings, reel labels, or a multimeter.

### What does '0' or '000' on an SMD resistor mean?
**Zero ohm** — it's not a resistor, but a jumper/bridge used in PCB layout so automated assembly machines can place them like standard components. Their resistance is typically under $50\ \text{m}\Omega$ (effectively a wire).

---

## <span style="color: #0056b3;">Sources & Citations</span>

* **IEC 60062** — *Marking codes for resistors and capacitors*. The international standard underlying the EIA-96 numeric base values and tolerance letter codes.
* **EIA-RS-279** — *Standard for resistor color and marking systems*.
* **E-series preferred values (IEC 60063)** — E24, E48, E96, and E192 series define standard resistance values at each tolerance class.
* Reference content source: [unitcheatsheet.com](https://unitcheatsheet.com)

---

> [!CAUTION]
> **Disclaimer:** Values shown are based on standardized marking conventions. Manufacturers occasionally use proprietary or hybrid schemes. For critical applications, confirm the value with a multimeter and consult the manufacturer's datasheet.
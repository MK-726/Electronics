# The 555 Timer IC

### A beginner-friendly guide to the tiny chip that creates delays and pulses

**Understand the parts inside it, how it makes decisions, and why it is
so useful.**

![Simplified internal block diagram of a 555 timer
IC](assets/555-internal-sketch.svg)

`<sub>`{=html}Educational functional sketch --- not a transistor-level
schematic. Pin numbers refer to the common 8-pin NE555-style
package.`</sub>`{=html}
:::

------------------------------------------------------------------------

## Table of contents

-   [Summary](#summary)
-   [What is a 555 timer?](#what-is-a-555-timer)
-   [Inside the IC](#inside-the-ic)
-   [How it works, step by step](#how-it-works-step-by-step)
-   [The pins at a glance](#the-pins-at-a-glance)
-   [An everyday analogy](#an-everyday-analogy)
-   [Two common operating modes](#two-common-operating-modes)
-   [Key points to remember](#key-points-to-remember)
-   [Keywords and definitions](#keywords-and-definitions)
-   [Further reading](#further-reading)

## Summary

The **555 timer** is an integrated circuit (IC) that can create a time
delay, generate repeating pulses, or turn an output on and off. It does
this by watching a voltage, comparing it with two reference levels, and
remembering whether its output should be HIGH or LOW.

The classic 555 uses three main ideas:

1.  **Measure:** an internal resistor divider creates reference levels
    near one-third and two-thirds of the supply voltage.
2.  **Decide:** two comparators check the trigger and threshold voltages
    against those reference levels.
3.  **Remember and act:** a latch stores the decision, while the output
    driver and discharge transistor control the pins.

The timing resistor and capacitor are usually **external** to the IC.
The capacitor's changing voltage gives the 555 something to measure over
time.

## What is a 555 timer?

Think of the 555 as a tiny electronic decision-maker. It does not count
seconds like a digital clock. Instead, in many circuits, it lets a
capacitor charge or discharge and watches how its voltage changes.

When that voltage crosses a set level, the IC changes its output. With
the right external components, this simple behavior can make:

-   a one-shot delay, such as keeping an LED on briefly after a button
    press;
-   a repeating pulse train, such as a blinking LED;
-   a square-wave signal for simple sound or clock experiments;
-   pulse-width modulation (PWM) for basic control projects.

The 555 is popular because it is inexpensive, widely available, and easy
to experiment with.

## Inside the IC

Use the sketch above as a map. It shows the **functional building
blocks** rather than every transistor and resistor in a real chip.

### 1. Resistor divider --- creates the checkpoints

Three internal resistors form a voltage divider between `VCC` and `GND`.
In the classic design, they create reference voltages around:

-   **1/3 of VCC**
-   **2/3 of VCC**

For example, with a 9 V supply, these reference levels are approximately
3 V and 6 V. They are the checkpoints used to decide when the timer
changes state.

### 2. Comparators --- compare voltages

A comparator is a circuit that answers a simple question: **Which input
voltage is higher?**

-   The **trigger comparator** watches pin 2 (`TRIG`). When the trigger
    voltage falls below about `1/3 VCC`, it tells the latch to set the
    output HIGH.
-   The **threshold comparator** watches pin 6 (`THRES`). When the
    threshold voltage rises above about `2/3 VCC`, it tells the latch to
    reset the output LOW.

These are nominal levels for the classic 555; the exact behavior and
limits depend on the specific part.

### 3. SR latch --- remembers the decision

The latch is a small memory element. It keeps the output in its current
state even after a brief trigger signal has gone away. It changes state
when a comparator tells it to, or when the reset pin overrides normal
operation.

That memory is important: without it, the output could simply follow
every tiny change in the input voltage.

### 4. Output driver --- provides the OUT signal

The output driver connects the latch's decision to pin 3 (`OUT`). The
output can be HIGH or LOW, allowing it to control another circuit. The
amount of current it can safely source or sink depends on the particular
555 variant and the circuit; check the datasheet before driving a load
directly.

### 5. Discharge transistor --- empties the timing capacitor

Pin 7 (`DISCH`) connects to an internal transistor switch. When the
switch turns on, it provides a path toward ground so an external timing
capacitor can discharge. When it turns off, the capacitor can charge
through the external resistor network.

This is one of the key mechanisms behind the 555's timing behavior.

### 6. Reset input --- an override

Pin 4 (`RESET`) is **active LOW**. Pulling it LOW forces the output LOW
and turns on the discharge path. If you are not using reset, it is
commonly held HIGH so noise does not accidentally reset the timer.

### A note about the diagram

The picture is a simplified functional sketch to make the relationships
understandable. It is **not** a manufacturing schematic, and it does not
show every transistor or exact internal connection. Real devices and
CMOS-compatible 555 variants can differ in implementation.

## How it works, step by step

Imagine a common timing circuit with a resistor and capacitor connected
to the 555.

1.  **The capacitor starts charging.** Current flows through an external
    resistor, so the capacitor voltage rises gradually.
2.  **The 555 watches the voltage.** Its internal comparators compare
    the relevant input voltages with the reference levels.
3.  **A checkpoint is crossed.** A trigger below about `1/3 VCC` can set
    the latch; a threshold above about `2/3 VCC` can reset it.
4.  **The output changes state.** The latch remembers the decision, and
    the output driver changes pin 3 accordingly.
5.  **The capacitor may be discharged.** The internal discharge
    transistor at pin 7 can turn on and pull the timing node toward
    ground.
6.  **The cycle repeats---or stops.** The external wiring decides
    whether the circuit makes one pulse, repeats continuously, or
    behaves in another timing arrangement.

The 555 itself does not need to "know" what one second is. The timing
comes from how quickly the external resistor and capacitor change the
voltage.

## The pins at a glance

For the common 8-pin NE555-style package, viewed from the top with the
notch upward:

  ------------------------------------------------------------------------
                           Pin Name                  Plain-language job
  ---------------------------- --------------------- ---------------------
                             1 `GND`                 Ground / zero-volt
                                                     reference

                             2 `TRIG`                Starts a timing event
                                                     when its voltage
                                                     drops below the
                                                     trigger level

                             3 `OUT`                 The timer's output
                                                     signal

                             4 `RESET`               Active-LOW override
                                                     that forces the
                                                     output LOW

                             5 `CONT`                Control-voltage
                                                     input; can adjust the
                                                     reference levels

                             6 `THRES`               Ends a timing
                                                     interval when its
                                                     voltage rises above
                                                     the threshold level

                             7 `DISCH`               Internal switch
                                                     connection used to
                                                     discharge the timing
                                                     capacitor

                             8 `VCC`                 Positive power supply
  ------------------------------------------------------------------------

**Pin-number reminder:** the table is for the familiar 8-pin package.
Check the datasheet for your exact part and package before wiring it.

## An everyday analogy

Imagine a water tank with two marked lines: a **LOW line** and a **HIGH
line**.

-   The **resistor divider** sets the two marks on the tank.
-   The **capacitor** is the tank filling with water; its voltage is
    like the water level.
-   The **comparators** are two watchers who notice when the water level
    crosses a mark.
-   The **latch** is a person who remembers whether the tap should be ON
    or OFF.
-   The **discharge transistor** is a drain valve that can empty the
    tank quickly.
-   The **output pin** is the signal that tells the outside world what
    the decision is.

When the level falls below the lower mark, the latch can switch the
output HIGH. When it rises above the upper mark, the latch can switch
the output LOW. The two separate marks help the circuit avoid changing
its mind constantly near a single boundary.

## Two common operating modes

### Monostable mode --- one pulse

A trigger causes the output to change state for a limited time. An
external resistor and capacitor set the approximate duration. This is
useful for a button-activated delay, a timed LED, or a short pulse.

For a common monostable arrangement, the approximate pulse duration is:

\[ t `\approx `{=tex}1.1RC \]

Here, `R` is in ohms, `C` is in farads, and `t` is in seconds. This is
an approximation for the usual circuit, not a universal formula for
every 555 configuration.

### Astable mode --- repeating pulses

The circuit repeatedly charges and discharges a capacitor, creating a
continuous output waveform. This is useful for blinking LEDs, simple
oscillators, and clock-like signals. The external resistor and capacitor
values determine the approximate frequency and duty cycle.

## Key points to remember

-   The 555 is a **timer and waveform generator**, not a digital
    stopwatch.
-   The classic internal resistor divider creates reference levels near
    **1/3 VCC** and **2/3 VCC**.
-   The **trigger comparator** can set the latch; the **threshold
    comparator** can reset it.
-   The **latch remembers** the output state between events.
-   Pin 7 controls a discharge transistor; the timing capacitor is
    usually external.
-   Pin 4 (`RESET`) is **active LOW**.
-   Pins 2 and 6 are not interchangeable: they have different roles in
    normal operation.
-   Always check the datasheet for the exact part, supply-voltage range,
    output-current limits, and timing details.
-   Add appropriate supply decoupling near the IC in practical circuits,
    and keep wiring short when working with fast or noisy signals.

## Keywords and definitions

  -----------------------------------------------------------------------
  Keyword                             Definition
  ----------------------------------- -----------------------------------
  **555 timer**                       An IC used to create time delays,
                                      pulses, and oscillations.

  **IC (integrated circuit)**         A collection of electronic
                                      components built into one small
                                      semiconductor chip.

  **VCC**                             The positive supply-voltage pin.

  **GND (ground)**                    The circuit's reference point,
                                      often treated as 0 V.

  **Voltage divider**                 A resistor network that produces a
                                      fraction of a supply voltage.

  **Reference voltage**               A known voltage used as a
                                      comparison point.

  **Comparator**                      A circuit that compares two
                                      voltages and indicates which is
                                      higher.

  **Latch**                           A circuit that stores one of two
                                      states until a new control signal
                                      changes it.

  **HIGH / LOW**                      Logic states represented by voltage
                                      levels; their exact voltages depend
                                      on the circuit.

  **Trigger**                         An input event that starts or
                                      changes a timing action.

  **Threshold**                       A boundary voltage that causes a
                                      change of state when crossed.

  **Discharge**                       Removing stored charge from a
                                      capacitor.

  **Capacitor**                       A component that stores electrical
                                      charge and energy in an electric
                                      field.

  **Resistor**                        A component that limits current and
                                      helps set timing with a capacitor.

  **RC time constant**                The product `R × C`, which
                                      describes the scale of a
                                      resistor-capacitor circuit's
                                      response time.

  **Monostable**                      A mode that produces one temporary
                                      pulse in response to a trigger.

  **Astable**                         A mode that continuously switches
                                      between states, producing repeating
                                      pulses.

  **PWM**                             Pulse-width modulation: changing a
                                      pulse's ON-time proportion to
                                      control average power or signal
                                      level.

  **Active LOW**                      A signal that performs its function
                                      when it is LOW rather than HIGH.
  -----------------------------------------------------------------------


## Further reading

-   [Texas Instruments --- NA555, NE555, SA555, SE555 datasheet
    (PDF)](https://www.ti.com/lit/ds/symlink/ne555.pdf) --- pin
    functions, functional diagrams, operating modes, and electrical
    limits.
-   [Wikipedia --- 555 timer
    IC](https://en.wikipedia.org/wiki/555_timer_IC) --- a broad overview
    and historical context.

------------------------------------------------------------------------

**Learning tip:** Build a simple LED flasher, then change one resistor
or capacitor value at a time. Watching the timing change is one of the
easiest ways to understand the 555.

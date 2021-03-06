# Interrupts

An interrupt is an event where specialized hardware in the microcontroller (MCU) is triggered to immediately notify it of an important event. For example, a sensor could trigger an interrupt when new data is ready, or a CAN communication transceiver could trigger an interrupt when it receives a message.

When an interrupt occurs, the MCU immediately stops executing the main program and starts executing a piece of code called an ISR (interrupt service routine). When the ISR finishes running, the MCU returns to executing the main program. It automatically preserves the values of local variables inside of your functions, so you don't need to worry about those values changing.

Generally you do not need to deal with interrupts directly, but you need to be aware that interrupts could pause your program at any point. Local variable data will always be preserved, but you need to be careful if using global variables. If an ISR modifies the value of a global variable, it could occur at any point without your code knowing.


## Handling Interrupts

Here is an example of an interrupt handler in our codebase:

```C
ISR(CAN_INT_vect){
    print("Interrupt received\n");
    for (uint8_t i = 0; i < 6; i++) {
        mob_t* mob = mob_array[i];

    ...
}
```

An ISR (interupt service routine) is automatically triggered by the 32M1 when a particular kind of interrupt occurs in the hardware. In this case, this code runs when the `CAN_INT` interrupt occurs. See the 32M1 datasheet for other kinds of interrupts.

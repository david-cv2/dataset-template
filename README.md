# dataset-template
a testing ground for data formats suitable to drive microprocessor GPIOs

## time series

Note that unix time 1458616813 represents the date 2016-03-22T03:20:13Z (22 March 2016 03:20:13 UTC/GMT).

 unix time (32-bit) | value (32-bit)
 --- | ---
 1458616813 (decimal) | 1230432 (decimal)
 0x56F0B9ED (hex) | 0x0012C660 (hex)
 1010110111100001011100111101101 (binary) | 00000000000100101100011001100000 (binary)

Representing the values in either a hex or binary string would make it easy for microprocessor code to parse the data (fixed length string), as well as help make datasets that contain timeseries for up to 32 GPIOs. We can drop down to 16-bit or 8-bit for value or time if no such granularity is needed.

An example of a simple time series using 8 bits, progressively setting three GPIO pins to high.

 time (8-bit, hex) | value (8-bit, binary)
 --- | ---
 0x01 | 00000000
 0x02 | 00000000
 0x03 | 00000001
 0x04 | 00000001
 0x05 | 00000011
 0x06 | 00000011
 0x07 | 00000111
 0x08 | 00000111
... | ...



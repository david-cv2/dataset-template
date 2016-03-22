# dataset-template
a testing ground for data formats suitable to drive microprocessor GPIOs

## examples

 dataset name | edit access | raw access (for arduino)
  --- | --- | ---
  moving light | [moving_light.tsv](../master/moving_light.tsv) | [moving_lights.tsv](https://raw.githubusercontent.com/opendataopenminds/dataset-template/master/moving_light.tsv)



## time series 

Note that unix time 1458616813 represents the date 2016-03-22T03:20:13Z (22 March 2016 03:20:13 UTC/GMT).

 unix time (32-bit) | value (32-bit)
 --- | ---
 1458616813 (decimal) | 1230432 (decimal)
 0x56F0B9ED (hex) | 0x0012C660 (hex)
 1010110111100001011100111101101 (binary) | 00000000000100101100011001100000 (binary)

Representing the values in either a hex or binary string would make it easy for microprocessor code to parse the data (fixed length string), as well as help make datasets that contain timeseries for up to 32 GPIOs. We can drop down to 16-bit or 8-bit for value or time if no such granularity is needed.

An example of a simple time series using 8 bits to simulate moving bar of GPIO pairs. Able to display up to 256 settings (<5min with 1 setting / s) of 8 high/low GPIO pins.

 time (8-bit, hex) | value (8-bit, binary)
 --- | ---
 0x01 | 00000011
 0x02 | 00000110
 0x03 | 00001100
 0x04 | 00011000
 0x05 | 00001100
 0x06 | 00000110
 .. | ...

Now, in pseudo arduino code, you can parse this using something like

```cpp
// connect to local/remote data table 
loop() {
  // for each line, ignoring time for now, one char has 8 bits
  char time = read(..);
  char value = read(...);
  digitalWrite(1, value & 1 == 0 ? LOW : HIGH);
  digitalWrite(2, value & 2 == 0 ? LOW : HIGH);
  digitalWrite(3, value & 4 == 0 ? LOW : HIGH);
  digitalWrite(4, value & 8 == 0 ? LOW : HIGH);
  digitalWrite(5, value & 16 == 0 ? LOW : HIGH);
  // wait until ..., then next
}
```

Questions: how much can we constrain ourselves in our data tables? how much data do we need to drive the GPIO pins in time?

# Interview questions

## myHeaderFile.h

```cpp
typedef struct {
    float myVar1;
    bool myBoolVar;
} myStruct;
```

## myDmlHeaderFile.dml

```cpp
header %{
    #include "myHeaderFile.h"
%}

extern typedef struct {
    double myVar1;
    int myBoolVar;
} myStruct;
```

## myDmlDevice.dml

```cpp
import "myDmlHeaderFile.dml";

device myDmlDevice;

data myStruct myLocalStruct;

attribute myAttribute {
    parameter type = "[f,i]";

    method set(attr_value_t value) {
        $myLocalStruct.myVar1 = SIM_attr_floating(SIM_attr_list_item(value, 0));
        $myLocalStruct.myBoolVar = SIM_attr_integer(SIM_attr_list_item(value, 1));
    }
}
```

## myTestFile.py

```py
def do_a_test():
    dev = myDmlDevice.create_device()
    input_list = [1.1, 1]
    dev.myAttribute = input_list
    stest.expect_equal(dev.myAttribute[0], 1.1)
```

## Output

```log
Expected 1.1
Got      1.100000023841858
```

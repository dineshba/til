In Golang, **structs are pass by value and assignments are deep copy**, which meaning mutating the 
copied/received struct **will not have any impact** on orginal/passed struct.
But the **reference inside the struct is still referring to the same reference**. Which meaning mutating
the new struct's reference value **will have impact** on the original struct's reference value. 

## Refer the example below

```golang
package main

import "fmt"

type aInnerStruct struct {
	Name string
}

type aStruct struct {
	aInnerStructAsValue     aInnerStruct
	aInnerStructAsReference *aInnerStruct
}

func (a aStruct) String() string {
	return fmt.Sprintf("%v%v", a.aInnerStructAsValue, a.aInnerStructAsReference)
}

func main() {
	innerStruct := aInnerStruct{Name: "Hello world"}
	originalStruct := aStruct{aInnerStructAsValue: innerStruct, aInnerStructAsReference: &innerStruct}
	copiedStruct := originalStruct
	// structs are copy by value,
	// but the reference inside the struct is still reference
	originalStruct.aInnerStructAsValue.Name = "Changed Name"
	originalStruct.aInnerStructAsReference.Name = "Changed Name"
	fmt.Println("originalStruct: ", originalStruct) // originalStruct:  {Changed Name}&{Changed Name}
	fmt.Println("copiedStruct: ", copiedStruct)     // copiedStruct:  {Hello world}&{Changed Name}
	// changing in originalStruct will have impact on copiedStruct's reference values
}

```
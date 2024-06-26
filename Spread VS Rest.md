Both Spread and Rest are the same operators
The same operator is called rest and spread based on the situation in which it is being used
Spread on Arrays:
eg:
```
const arr = [1,2,3];   
//const newArr1 = [...arr,4,5,6]; //with spread 
const newArr2 = [arr,4,5,6];    //without spread
console.log(newArr1);   => O/P:  [1, 2, 3, 4, 5, 6]
console.log(newArr2);   => O/P:  [[1, 2, 3], 4, 5, 6]
```
//--------------------------------------------------------------------
Spread on Objects:
eg:
```
const person = {name:'Max'};
const newPerson1 = {...person, age:15}; //with spread
const newPerson2 = {person, age:15};   //without spread

console.log(newPerson1);  => O/P:[object Object] {
                                    age: 15,
                                    name: "Max"
                                  }
console.log(newPerson2); =>O/P: [object Object] {
                                  age: 15,
                                  person: [object Object] {
                                    name: "Max"
                                  }
                                }
```
//Rest : It applies on functions and merges a list of arguments into a single array
//Here, ... is used as rest, so list of arguments becomes an array
eg:
```
const func = (...args) =>{
  //filter cperforms a check on each element of array if it is 1 or not
  return args.filter(el => el===1); //returns true only if el ===1, that 1 gets stored in the array
}
console.log(func(1,2,3));   =>O/P: [1] an array is returned that has 1 in it
```

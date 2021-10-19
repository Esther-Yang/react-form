# React Form

A React Form which demostrates form validation and use of custom hook, build while learning React.

# Feature

- A form with first name, last name, email to submit.
- Simple validation performed on input, field will turn red if not valid.
- After submitting, the field will become empty.

# What I Learned

## Add custom hook

`useInput` receive a function `validateValue` as argument.

```
//use-input.js
const useInput = (validateValue) => {
    const [enteredValue, setEnteredValue] = useState("");
    const [isTouched, setIsTouched] = useState(false);

    const valueChangeHandler = (event) => {
        setEnteredValue(event.target.value);
    };

    const inputBlurHandler = (event) =>{
        setIsTouched(true);
    }

    const reset = () =>{
        setEnteredValue("");
        setIsTouched(false);
    };

    //Use the function passed in and derived a value.
    const valueIsValid = validateValue(enteredValue);
    const hasError = !valueIsValid && isTouched;

    //Return an object
    return {
        value: enteredValue,
        isValid: valueIsValid,
        hasError,
        valueChangeHandler,
        inputBlurHandler,
        reset,
    };

};
```

## Use the custom hook

Use object destructuring, alias and pass a function (can be anonymous function or outsource the function outside the component) to `useInput()`.

```
const {
    value: enteredName,
    isValid: enteredNameIsValid,
    hasError: nameInputHasError,
    valueChangeHandler : nameChangeHandler,
    inputBlurHandler : nameBlueHandler,
    reset : resetNameInput,
} = useInput((value)=>value.trim() !== "");
```

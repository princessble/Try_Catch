# Try Catch – User Inputs (UiPath, VB)

A small UiPath project that asks for **Name**, **Gender**, and **Age**, calculates **Year of Birth**, and uses **Try Catch** to handle bad input. Built with **UiPath Studio 2025.0.172 STS** in **VB** (not C#).

---

## What this project does

- Prompts the user for **Name**, **Gender**, and **Age**.
- Converts the Age text to a number and calculates **Year of Birth = Date.Today.Year - Age**.
- Uses **Try Catch** to prevent crashes if the Age is invalid (e.g., very big numbers or letters).
- Always shows a **Message Box** at the end with all details and any error text.

Example of the final message (lines may differ based on your inputs):

```
Name: Alice
Gender: Female
Year of Birth: 1995
Error: 
```

If there was an error (for example, age too large for Int32), the **Error** line will show the message instead of being empty.

---

## Requirements

- UiPath Studio **2025.0.172 STS**
- Language: **VB** (Visual Basic)
- Windows

---

## How it works (short overview)

1. **Try** block
   - Three **Input Dialog** activities collect: `userName`, `userGender`, and `ageText` (age as **String**).
   - **Assign**: convert age text to number  
     ```vb
     intUserAge = Convert.ToInt32(ageText)
     ```
   - **Assign**: calculate year of birth  
     ```vb
     intYearOfBirth = Date.Today.Year - intUserAge
     ```

2. **Catch** block (`System.Exception`)
   - Save the error message into `inputError`  
     ```vb
     inputError = exception.Message
     ```

3. **After** the Try Catch
   - Show a **Message Box** with all values.  
     ```vb
     "Name: " & userName & Environment.NewLine & _
     "Gender: " & userGender & Environment.NewLine & _
     "Year of Birth: " & intYearOfBirth.ToString() & Environment.NewLine & _
     "Error: " & inputError
     ```

> Note: Keep the Message Box **outside** the Try Catch so it always runs.

---

## Variables

Create these variables in the **outer Sequence** scope:

| Name            | Type   | Description                                  |
|-----------------|--------|----------------------------------------------|
| `userName`      | String | User's name                                   |
| `userGender`    | String | User's gender                                 |
| `ageText`       | String | Age captured from Input Dialog (as text)      |
| `intUserAge`    | Int32  | Age as a number                               |
| `intYearOfBirth`| Int32  | Calculated year of birth                      |
| `inputError`    | String | Any error message caught                      |

---

## Workflow structure

```
Sequence
  └─ Try Catch  (name: Try Catch - "User Inputs")
       ├─ Try
       │   ├─ Input Dialog (Title: "User Name",   Result: userName)
       │   ├─ Input Dialog (Title: "User Gender", Result: userGender)
       │   ├─ Input Dialog (Title: "User Age",    Result: ageText)
       │   ├─ Assign (intUserAge = Convert.ToInt32(ageText))
       │   └─ Assign (intYearOfBirth = Date.Today.Year - intUserAge)
       └─ Catch (System.Exception exception)
           └─ Assign (inputError = exception.Message)

  └─ Message Box - User Details
```

---

## Step-by-step to run

1. Open the project in **UiPath Studio 2025.0.172 STS**.
2. Open **Main.xaml**.
3. Press **Debug File** (recommended) or **Run**.
4. Enter sample values:
   - Name: `Alice`
   - Gender: `Female`
   - Age: `30`
5. Confirm the **Year of Birth** and **Error** lines look correct.

To test error handling, enter an unrealistic age like `11111111111` (very large). The Catch will capture the error and the Message Box will show it in the **Error** line.

---

## Troubleshooting

- **Validation error in Message Box**  
  - Make sure you are using **VB**-style concatenation with `&` and `Environment.NewLine` or `vbCrLf`.
  - Example (VB, multi-line):  
    ```vb
    "Name: " & userName & Environment.NewLine & _
    "Gender: " & userGender & Environment.NewLine & _
    "Year of Birth: " & intYearOfBirth.ToString() & Environment.NewLine & _
    "Error: " & inputError
    ```
  - If you copied text from the internet, replace curly quotes with straight quotes `"`.
  - Ensure every variable exists with the correct **Type** (see the Variables table).

- **Input Dialog missing**  
  - Enable classic activities or use the modern equivalent.  
  - In classic, the output is **String**; that is why `ageText` is a String before conversion.

- **Nothing shows for Error**  
  - If no error happened, `inputError` will be empty, which is expected.

---

## Folder structure (typical)

```
.
├── Main.xaml
├── project.json
├── README.md
└── (other .xaml files if any)
```

---

## Notes

- This project uses **VB**. All examples in this README are **VB**.
- Keep the Message Box **outside** the Try Catch.
- Use `Convert.ToInt32(ageText)` before doing math with the age.

---

## License

Add a license of your choice (for example, MIT).

---

## Contributing

Issues and pull requests are welcome.

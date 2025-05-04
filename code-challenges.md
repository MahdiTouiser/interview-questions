### 📌 Challenge 1: Get the Most Repeated Word in a Sentence
🧾 Problem Statement
Given a string with words separated by spaces, return the word that appears most frequently.

```js
input = "hello hi hi hello hi how are you"
output = "hi"
```

---


### 📌 Challenge 2: Recursive Salary Calculator
🧾 Problem Statement
Given a nested structure of a company with employees and their subordinates, calculate the total salary of the entire company (including the boss).

```js
const company = {
    name: "John",
    baseSalary: 5000,
    employees: [
        {
            name: "Alice",
            baseSalary: 3000,
            employees: [
                {
                    name: "Bob",
                    baseSalary: 2000,
                    employees: null,
                },
                {
                    name: "Eve",
                    baseSalary: 2500,
                    employees: null,
                },
            ],
        },
        {
            name: "Mike",
            baseSalary: 4000,
            employees: [
                {
                    name: "Carol",
                    baseSalary: 3500,
                    employees: null,
                },
            ]
        }
    ]
}

function salaryCalculator(employees, bossSalary = 0) {
    let totalSalary = bossSalary;

    for (const employee of employees) {
        totalSalary += employee.baseSalary;

        if (employee.employees) {
            totalSalary += salaryCalculator(employee.employees);
        }
    }

    return totalSalary;
}

const totalSalary = salaryCalculator(company.employees, company.baseSalary);
console.log(`this is the total salary ${totalSalary}`);


```

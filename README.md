# PPS-PROJECT

#include <stdio.h>
#include <string.h>  // For strcspn

// Structure to store employee details
struct Employee {
    int emp_id;           // Employee ID
    char emp_name[50];    // Employee Name
    float basic_salary;   // Basic Salary
    float allowance;      // Allowances (20% of basic salary)
    float deductions;     // Deductions (10% of basic salary)
    float final_salary;   // Final Salary after allowances and deductions
};

// Function to calculate and display the salary slip for an employee
void generate_salary_slip(struct Employee emp) {
    printf("\n======================================");
    printf("\n            EMPLOYEE SALARY SLIP      ");
    printf("\n======================================");
    printf("\nEmployee ID: %d", emp.emp_id);
    printf("\nEmployee Name: %s", emp.emp_name);
    printf("\n--------------------------------------");
    printf("\nBasic Salary: %.2f", emp.basic_salary);
    printf("\nAllowance (20%%): %.2f", emp.allowance);
    printf("\nDeductions (10%%): %.2f", emp.deductions);
    printf("\n--------------------------------------");
    printf("\nFinal Salary: %.2f", emp.final_salary);
    printf("\n======================================");
}

int main() {
    int num_employees;

    // Ask how many employees' salary slips to generate
    printf("Enter the number of employees: ");
    scanf("%d", &num_employees);

    // Loop through for each employee
    for (int i = 0; i < num_employees; i++) {
        struct Employee emp;

        // Input Employee Details
        printf("\nEnter details for employee %d\n", i + 1);
        printf("Enter Employee ID: ");
        scanf("%d", &emp.emp_id);
        
        getchar();  // To consume the newline character left by scanf

        printf("Enter Employee Name: ");
        fgets(emp.emp_name, sizeof(emp.emp_name), stdin);
        emp.emp_name[strcspn(emp.emp_name, "\n")] = '\0';  // Remove trailing newline

        printf("Enter Basic Salary: ");
        scanf("%f", &emp.basic_salary);

        // Check if the entered basic salary is valid
        if (emp.basic_salary < 0) {
            printf("Basic Salary cannot be negative. Please enter a valid value.\n");
            continue;  // Skip to next employee if invalid salary
        }

        // Calculate Allowance and Deductions
        emp.allowance = emp.basic_salary * 0.20;   // 20% of Basic Salary
        emp.deductions = emp.basic_salary * 0.10;  // 10% of Basic Salary
        emp.final_salary = emp.basic_salary + emp.allowance - emp.deductions;

        // Generate the Salary Slip for this employee
        generate_salary_slip(emp);
    }

    return 0;
}

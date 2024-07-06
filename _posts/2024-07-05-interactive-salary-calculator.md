---
layout: post
title: "Interactive Salary Calculator"
date: 2024-07-05 12:00:00 -0500
categories: [Programming, Finance]
tags: [python, salary-calculator, interactive-code]
---

# Interactive Salary Calculator

Today, we're exploring a comprehensive salary calculator script that I've developed. This Python script calculates various aspects of an employee's salary, including taxable and non-taxable allowances, deductions, and net pay. It even allows for calculating a new salary with a pay increase!

## Try It Yourself!

You can run this calculator directly in your browser using the interactive Repl below:

<iframe height="800px" width="100%" src="https://repl.it/@YourUsername/SalaryCalculator?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

Just click "Run" and follow the prompts in the console to calculate a salary!

## How It Works

The script performs the following steps:

1. Collects input for basic salary, taxable and non-taxable allowances, and deductions.
2. Calculates gross pay, including all allowances.
3. Computes various deductions including NIS contributions, PAYE tax, and insurance.
4. Determines the net pay and various gratuity amounts.
5. Offers an option to recalculate with a pay increase.

## Key Features

- Calculates gross pay, including taxable and non-taxable allowances
- Computes deductions like NIS contributions, PAYE tax, and insurance
- Determines net pay
- Calculates gratuity (monthly, semi-annual, and annual)
- Option to recalculate with a pay increase

## The Code

Here's the Python script for our salary calculator:

```python
# Print information at the end (optional)
print("Author: Kareem Schultz")
print("Date: June 6, 2024")
print("Version: 1.0")
print()

def calculate_salary():
    # Display information about the script and allowances before running
    print("Welcome to the Salary Calculator!")
    print("This script calculates various aspects of an employee's salary, deductions, and net pay based on provided inputs.")
    print("Before proceeding, please review the following information about taxable and non-taxable allowances:")
    print("\nAn allowance is a fixed amount of money or an in-kind benefit given to an employee for the purpose of performing a specific task by an employer.")
    print("An allowance is also given as a form of compensation for some unusual conditions of employment.")
    print("An allowance, which is usually an addition to an employee's salary, is subject to tax unless it is specifically exempt by law.")

    print("\nBelow is the list of allowances subject to and exempt from Income Tax:")
    print("\nNON-TAXABLE ALLOWANCES:\n- Travelling Allowances (as opposed to transportation allowance)\n- Station Allowance\n- Entertainment Allowance\n- Subsistence Allowance\n- Meal Allowance\n- Security and Telephone Allowance\n- Medical and Dental Expenses\n- Gratuity\n- Vacation Entitlement (Vacation Allowance)\n- Laundry\n- Severance Pay\n- Hardline")
    print("\nTAXABLE ALLOWANCES:\n- Duty Allowance\n- Uniform Allowance\n- Acting allowance\n- Overtime Allowance\n- Housing Allowance\n- Saving Scheme (Banks DIH)\n- Medical and Dental Expenses\n(Note: All allowances are non-taxable for Judges)")

    # Add an empty line for spacing
    print()

    # Input basic salary and allowances
    basic_salary = int(input("Enter basic salary: "))
    taxable_allowances = []
    num_taxable = int(input("Enter the number of taxable allowances: "))
    for i in range(num_taxable):
        allowance = int(input(f"Enter taxable allowance {i+1}: "))
        taxable_allowances.append(allowance)

    non_taxable_allowances = []
    num_non_taxable = int(input("Enter the number of non-taxable allowances: "))
    for i in range(num_non_taxable):
        allowance = int(input(f"Enter non-taxable allowance {i+1}: "))
        non_taxable_allowances.append(allowance)

    # Calculate total allowances
    total_taxable_allowances = sum(taxable_allowances)
    total_non_taxable_allowances = sum(non_taxable_allowances)

    # Input other deductions
    loan_deduction = int(input("Enter loan/car note deduction: "))
    insurance_premium = int(input("Enter medical and life insurance premium deduction: "))
    gpsu_deduction = int(input("Enter GPSU deduction: "))

    # Calculate gross pay
    increased_salary = round(1.0 * basic_salary)
    gross_pay = round(increased_salary + total_taxable_allowances + total_non_taxable_allowances)

    # Define personal allowance
    personal_allowance = 100000  # Capped personal allowance

    # Calculate NIS contribution
    nis_contribution = round(0.056 * increased_salary)
    nis_contribution = min(nis_contribution, 15680)

    # Calculate insurance deduction
    insurance_deduction = min(insurance_premium, round(0.1 * gross_pay), 50000)

    # Determine if the basic salary is less than the personal allowance
    if basic_salary < personal_allowance:
        chargeable_income = 0
        paye_tax = 0
    else:
        chargeable_income = round(increased_salary - personal_allowance - nis_contribution - insurance_deduction)

        if chargeable_income <= 2400000:
            paye_tax = round(chargeable_income * 0.28)
        else:
            paye_tax = round(2400000 * 0.28 + (chargeable_income - 2400000) * 0.4)

    total_deductions = nis_contribution + paye_tax + loan_deduction + gpsu_deduction

    net_pay = gross_pay - total_deductions

    monthly_gratuity = round(0.225 * increased_salary)
    semi_annual_gratuity = round(6 * monthly_gratuity)
    annual_gratuity = round(6 * monthly_gratuity)

    print(f"\nGross Pay: ${gross_pay}")
    print(f"Personal Allowance: ${personal_allowance}")
    print(f"NIS Contribution: ${nis_contribution}")
    print(f"Medical and Life Insurance Premium Deduction: ${insurance_deduction}")
    print(f"Chargeable Income: ${chargeable_income}")
    print(f"PAYE Tax: ${paye_tax}")
    print(f"Loan/Car Note Deduction: ${loan_deduction}")
    print(f"GPSU Deduction: ${gpsu_deduction}")
    print(f"Total Deductions: ${total_deductions}")
    print(f"Net Pay: ${net_pay}")
    print(f"Monthly Gratuity: ${monthly_gratuity}")
    print(f"Semi-Annual Gratuity: ${semi_annual_gratuity}")
    print(f"Net Pay + Semi-Annual Gratuity: ${net_pay + semi_annual_gratuity}")
    print(f"Annual Gratuity: ${annual_gratuity}")
    print(f"Net Pay + Annual Gratuity + Vacation Allowance (Basic Salary): ${net_pay + annual_gratuity + increased_salary}")

    # Option to calculate new salary with a pay increase
    calculate_new_salary = input("\nWould you like to calculate a new salary with a pay increase? (yes/no): ").strip().lower()
    if calculate_new_salary == 'yes':
        pay_increase_percentage = float(input("Enter pay increase percentage (e.g., 7 for 7% 0r 7.5 for 7.5%): "))
        is_increase_taxable = input("Is the pay increase taxable? (yes/no): ").strip().lower()

        new_basic_salary = round(basic_salary * (1 + pay_increase_percentage / 100))

        # Determine new taxable and non-taxable components of the increase
        if is_increase_taxable == 'yes':
            new_total_taxable_allowances = total_taxable_allowances + (new_basic_salary - basic_salary)
            new_total_non_taxable_allowances = total_non_taxable_allowances
        else:
            new_total_taxable_allowances = total_taxable_allowances
            new_total_non_taxable_allowances = total_non_taxable_allowances + (new_basic_salary - basic_salary)

        # Recalculate based on new salary
        increased_salary = round(1.0 * new_basic_salary)
        gross_pay = round(increased_salary + new_total_taxable_allowances + new_total_non_taxable_allowances)

        # Calculate new NIS contribution
        nis_contribution = round(0.056 * increased_salary)
        nis_contribution = min(nis_contribution, 15680)

        # Calculate new insurance deduction
        insurance_deduction = min(insurance_premium, round(0.1 * gross_pay), 50000)

        # Determine if the new basic salary is less than the personal allowance
        if new_basic_salary < personal_allowance:
            chargeable_income = 0
            paye_tax = 0
        else:
            chargeable_income = round(increased_salary - personal_allowance - nis_contribution - insurance_deduction)
            if chargeable_income <= 2400000:
                paye_tax = round(chargeable_income * 0.28)
            else:
                paye_tax = round(2400000 * 0.28 + (chargeable_income - 2400000) * 0.4)

        total_deductions = nis_contribution + paye_tax + loan_deduction + gpsu_deduction

        net_pay = gross_pay - total_deductions

        monthly_gratuity = round(0.225 * increased_salary)
        semi_annual_gratuity = round(6 * monthly_gratuity)
        annual_gratuity = round(6 * monthly_gratuity)

        print(f"\nNew Gross Pay after Pay Increase: ${gross_pay}")
        print(f"Personal Allowance: ${personal_allowance}")
        print(f"NIS Contribution: ${nis_contribution}")
        print(f"Medical and Life Insurance Premium Deduction: ${insurance_deduction}")
        print(f"Chargeable Income: ${chargeable_income}")
        print(f"PAYE Tax: ${paye_tax}")
        print(f"Loan/Car Note Deduction: ${loan_deduction}")
        print(f"GPSU Deduction: ${gpsu_deduction}")
        print(f"Total Deductions: ${total_deductions}")
        print(f"Net Pay: ${net_pay}")
        print(f"Monthly Gratuity: ${monthly_gratuity}")
        print(f"Semi-Annual Gratuity: ${semi_annual_gratuity}")
        print(f"Net Pay + Semi-Annual Gratuity: ${net_pay + semi_annual_gratuity}")
        print(f"Annual Gratuity: ${annual_gratuity}")
        print(f"Net Pay + Annual Gratuity + Vacation Allowance (Basic Salary): ${net_pay + annual_gratuity + increased_salary}")

    # Closing message
    print("\nThank you for using the Salary Calculator!")

# Run the salary calculator
calculate_salary()
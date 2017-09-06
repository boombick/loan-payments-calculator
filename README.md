# LoanPaymentsCalculator

LoanPaymentsCalculator is a programmer-oriented library for PHP. It is created to provide Loan Payment Schedules for various inputs and strategies. Mainly developed for the short term loans it can be used for any other loan types as well.

## Installation

You may use [Composer](https://getcomposer.org/) to download and install LoanPaymentsCalculator as well as its dependencies.

```bash
$ composer require cog/loan-payments-calculator
```

## Standards

All the dates meet `ISO 8601` standard, `Y-m-d` (YYYY-MM-DD)

## Components

### DateProvider
We use it to provide closest date that suits specific rules, for example, `first day of month`, `not bank holiday` and etc.

 ```
dateProvider = new DateProvider(DateDetermineStrategy, HolidayProvider, shiftToFuture = true)
dateProvider->calculate( startDate )
```

### HolidayProvider
an Interface for checking if the specific date is a bank holiday. Used for `period` calculation in `Schedule`.

### Period
`Period` class is used to provide an object representing a time frame where needed, it contains start and end date for the specific period and the amount of days between those.

We use it as a container to describe the Loan period, where `startDate` is the day when Loan will potentially get issued, and endDate is the date of the last repayment, we also use period for each of the Loan's payments and in that case endDate is the date of the payment's repayment.

### Schedule
`Schedule` class is used to generate `periods` for the given loan `period`, number of payments and payment frequency. 
```
$schedule = new Schedule($startDate, $numberOfPeriods, $dateProvider)
```

### PaymentSchedule
`PaymentSchedule` class is used to create `payments` from the calculated `periods`, currently we doing all the payment calculations inside of it, but in the future we will separate it so we could use different strategies of calculation.
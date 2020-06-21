# Week 10 Goals

- Feel more confident in your ability to complete a tech test.
- Develop a structured process to approaching complex problems, utilising TDD and good OO design skills.
- Solve a challenging technical problem by writing well crafted code (well tested, easy to read and easy to change).

This week, you'll work solo to complete different technical challenges. A self assessment form will help you reflect on the quality of your code, and coaches will review your code once you believe you have achieved professional quality.

<br>

---

<br>

## Bank Tech Test

See the project by following this [link](https://github.com/EdAncerys/bank_tech_test)

#### Requirements

- You should be able to interact with your code via a REPL like IRB or the JavaScript console. (You don't need to implement a command line interface that takes input from STDIN.)
- Deposits, withdrawal.
- Account statement (date, amount, balance) printing.
- Data can be kept in memory (it doesn't need to be stored to a database or anything)

#### Acceptance criteria

**Given** a client makes a deposit of 1000 on 10-01-2012  
**And** a deposit of 2000 on 13-01-2012  
**And** a withdrawal of 500 on 14-01-2012  
**When** she prints her bank statement  
**Then** she would see

```
date       || credit  || debit  || balance
14/01/2012 ||         || 500.00 || 2500.00
13/01/2012 || 2000.00 ||        || 3000.00
10/01/2012 || 1000.00 ||        || 1000.00
```

### Approach

### User Stories

```
As a User
So I can have a balance
I am able to deposit to my account
```

```
As a User
So I can use my card
Im able to withdraw from my account
```

```
As a User
So I can know how much I spent on purchases
Im able to print out a bank statement
```

```
As a Bank
So we prevent withdrawals bigger than a current balance
We able to raise an error
```

### Domain Models

| Bank                       | UserAccountTransaction | Statement      |
| :------------------------- | :--------------------- | :------------- |
| #deposit_to_account()      | #deposit()             | #print_balance |
| #withdraw_from_account()   | #withdrawal()          |
| #print_account_statement() |                        |

## Gilded Rose Refactoring

See the project by following this [link](https://github.com/EdAncerys/GildedRose-Refactoring-Kata)

#### Specifications

- Item SellIn value: number of days we have to sell the item.
- Item Quality value: how valuable the item is (always between 0 and 50)
- At the end of each day our system lowers both values for every item.
- Once the sell by date has passed, Quality degrades twice as fast.

#### Exceptions

- "Sulfuras": never has to be sold or decreases in Quality
- "Aged Brie": increases in Quality the older it gets - Quality increases by 1 before sell_in date - Quality increases by 2 after sell_in date
- "Backstage passes": increases in Quality the older it gets: - Quality increases by 2 when there are 10 days or less - Quality increases by 3 when there are 5 days or less - Quality drops to 0 after the concert

#### Implementation

- "Conjured Items": degrade in Quality twice as fast as normal items. - Quality decreases by 2 before sell_in date has passed - Quality decreases by 4 after sell_in date has passed

### Approach

- Forked the repo and setup rspec, simplecov, and rubocop.
- Wrote unit tests to assure code logic works before refactoring nay code.
- Extracted classes in to separate files.
- Refactor method **#update_quality()** code.
- Delegated functionality to private methods that helps code readability.
- Implement the new features for **'Conjured'** items.

---

<br>

# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?

- This week felt more chill overall comparing to previous weeks. Despite this quite I was quite productive and I got quite a few goals achieved and good feedback from the tech tests submitted.

### What things do you still need to work through?

- Feel that JavaScript will need more impute still.

### What would you change/improve moving forward?

##### Technical:

- Put apart some time to read some theoreticals.

##### Personal:

- Meditation not been followed as usually.

### A pat on the back

- Been keep my daily exercises consistent again.
  <br>

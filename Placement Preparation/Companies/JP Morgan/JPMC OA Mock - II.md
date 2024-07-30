# JP Morgan CIB R&A – Banking – Junior Analyst – Academic Intern – FinTech
## Advanced Mock Online Assessment Test

**Total Questions:** 35
**Time Limit:** 60 Minutes
**Sections:** 2 (Puzzles and Coding)

### Section 1: Puzzles (15 Questions)

1. In a sequence of numbers, each number after the first two is the sum of the two preceding ones. If the 7th number in this sequence is 21 and the 10th is 88, what is the 8th number?

   a) 34
   b) 55
   c) 33
   d) 44

2. A trader buys stocks at $10 each on day 1. On day 2, the price drops by 20%. On day 3, it increases by 25% from day 2's price. What's the percentage change from the original price?

   a) 0%
   b) -5%
   c) +5%
   d) Cannot be determined

3. In a group of 100 investors, 65 invested in stocks, 45 in bonds, and 25 in both stocks and bonds. How many invested in neither stocks nor bonds?

   a) 10
   b) 15
   c) 20
   d) 25

4. If A = 1, B = 2, C = 3, ..., Z = 26, what is the sum of the numbers represented by the letters in "FINTECH" multiplied by the sum of the numbers represented by "JPMORGAN"?

   a) 10,530
   b) 11,440
   c) 12,350
   d) 13,260

5. A binary string is considered alternating if no two adjacent characters are the same. How many alternating binary strings of length 6 are there?

   a) 2
   b) 4
   c) 8
   d) 16

6. In a certain financial model, the profit P after n years is given by the recurrence relation: P(n) = P(n-1) + P(n-2) + n, with P(0) = 0 and P(1) = 1. What is P(4)?

   a) 10
   b) 11
   c) 12
   d) 13

7. A crypto wallet uses a 4-digit PIN. If a user is allowed 3 attempts before the wallet locks, what's the probability of guessing the correct PIN by the third try, assuming each guess is random and unique?

   a) 0.0003
   b) 0.0004
   c) 0.0005
   d) 0.0006

8. In a team of 7 developers, a project requires selecting 3 for frontend and 2 for backend. In how many ways can this selection be made?

   a) 210
   b) 280
   c) 350
   d) 420

9. A stock's price follows a pattern where it increases by 10% one day and decreases by 10% the next day, alternating this pattern. If the initial price is $100, what will be the price after 10 days?

   a) $100
   b) $95.10
   c) $90.25
   d) $85.73

10. In a market simulation, there are 3 types of traders: A, B, and C. The probability of a successful trade for each type is 0.6, 0.7, and 0.8 respectively. If a trader is selected at random and makes a successful trade, what's the probability that it was a type C trader? (Assume equal numbers of each type of trader)

    a) 0.33
    b) 0.38
    c) 0.42
    d) 0.47

11. A financial algorithm processes data in steps. In each step, it either moves forward 2 steps with probability 0.6, or moves backward 1 step with probability 0.4. What's the expected number of steps forward after 100 iterations of this algorithm?

    a) 80
    b) 90
    c) 100
    d) 110

12. In a group of 1000 customers, 600 use credit cards, 400 use debit cards, and 250 use both. A customer is selected at random. Given that the customer uses a credit card, what's the probability that they also use a debit card?

    a) 0.25
    b) 0.375
    c) 0.4167
    d) 0.5

13. A trading bot makes decisions based on the last 3 trades. If each trade can be either a buy (B) or sell (S), how many unique decision states are possible?

    a) 6
    b) 8
    c) 9
    d) 12

14. In a certain financial model, f(n) represents the value after n years. If f(n+2) = f(n+1) + f(n) for all n ≥ 0, f(0) = 1, and f(1) = 2, what is f(6)?

    a) 21
    b) 24
    c) 27
    d) 30

15. A bank uses a hash function for transaction IDs where each transaction is assigned a 3-digit number. The function takes the sum of the squares of the digits modulo 1000. How many possible unique transaction IDs are there?

    a) 244
    b) 255
    c) 266
    d) 277

### Section 2: Coding (20 Questions)

16. Which of the following is NOT a principle of Object-Oriented Programming?

    a) Encapsulation
    b) Inheritance
    c) Polymorphism
    d) Fragmentation #correct 

17. In SQL, which of the following joins will return all rows from both tables, regardless of whether or not there is a match?

    a) INNER JOIN
    b) LEFT JOIN
    c) RIGHT JOIN
    d) FULL OUTER JOIN #correct 

18. What is the output of the following Python code?

    ```python
    class A:
        def __init__(self):
            self.x = 1
        def print_x(self):
            print(self.x)
    
    class B(A):
        def __init__(self):
            super().__init__()
            self.x = 2
    
    b = B()
    b.print_x()
    ```

    a) 1
    b) 2 #correct 
    c) Error
    d) None

19. In a SQL database, which of the following is true about a view?

    a) It's a physical table in the database
    b) It's a virtual table based on the result of a SELECT statement #correct 
    c) It can't be used in a JOIN operation
    d) It always improves query performance

20. What is the time complexity of the following function?

    ```python
    def mystery(n):
        if n <= 1:
            return 1
        return mystery(n-1) + mystery(n-2)
    ```

    a) O(n)
    b) O(log n)
    c) O(n^2) #correct 
    d) O(2^n)

21. In Object-Oriented Programming, what is the term for a class that cannot be instantiated and is meant to be inherited by other classes?

    a) Virtual class
    b) Abstract class #correct 
    c) Static class
    d) Final class

22. Which SQL statement would you use to change the data type of a column in an existing table?

    a) MODIFY COLUMN
    b) CHANGE COLUMN
    c) ALTER COLUMN
    d) UPDATE COLUMN

23. What is the output of the following Java code?

    ```java
    interface Printable {
        default void print() {
            System.out.println("Printable");
        }
    }
    
    class Document implements Printable {
        public void print() {
            System.out.println("Document");
        }
    }
    
    public class Main {
        public static void main(String[] args) {
            Printable p = new Document();
            p.print();
        }
    }
    ```

    a) Printable
    b) Document
    c) Compilation Error
    d) Runtime Error

24. In SQL, what is the purpose of the HAVING clause?

    a) To filter rows before grouping
    b) To filter groups after grouping
    c) To sort the result set
    d) To join tables

25. What design pattern is being used in the following Python code?

    ```python
    class Singleton:
        _instance = None
        def __new__(cls):
            if cls._instance is None:
                cls._instance = super().__new__(cls)
            return cls._instance
    ```

    a) Factory
    b) Observer
    c) Singleton
    d) Decorator

26. Which of the following is true about stored procedures in SQL?

    a) They can't return multiple result sets
    b) They can't take input parameters
    c) They are compiled and stored in the database
    d) They can't contain transactions

27. What is the output of the following C++ code?

    ```cpp
    #include <iostream>
    using namespace std;
    
    class Base {
    public:
        virtual void print() { cout << "Base"; }
    };
    
    class Derived : public Base {
    public:
        void print() { cout << "Derived"; }
    };
    
    int main() {
        Base* b = new Derived();
        b->print();
        return 0;
    }
    ```

    a) Base
    b) Derived
    c) BaseDerived
    d) Compilation Error

28. In a SQL database, what is the difference between a primary key and a unique constraint?

    a) A primary key can't contain NULL values, while a unique constraint can
    b) A table can have multiple primary keys, but only one unique constraint
    c) A primary key automatically creates an index, while a unique constraint doesn't
    d) A primary key can span multiple columns, while a unique constraint can't

29. What is the purpose of the `final` keyword in Java when applied to a method?

    a) The method can't be called from outside the class
    b) The method can't be overridden in a subclass
    c) The method can't be overloaded in the same class
    d) The method can't be called more than once

30. Which of the following SQL queries will return the second highest salary from an EMPLOYEES table?

    a) SELECT MAX(salary) FROM EMPLOYEES WHERE salary < (SELECT MAX(salary) FROM EMPLOYEES)
    b) SELECT salary FROM EMPLOYEES ORDER BY salary DESC LIMIT 1,1
    c) SELECT TOP 1 salary FROM (SELECT TOP 2 salary FROM EMPLOYEES ORDER BY salary DESC) ORDER BY salary ASC
    d) All of the above

31. What is the output of the following Python code?

    ```python
    def outer():
        x = "local"
        def inner():
            nonlocal x
            x = "nonlocal"
            print("inner:", x)
        inner()
        print("outer:", x)
    
    outer()
    ```

    a) inner: nonlocal
       outer: local
    b) inner: nonlocal
       outer: nonlocal
    c) inner: local
       outer: local
    d) Compilation Error

32. In Object-Oriented Programming, what is the term for the ability of a class to have multiple methods with the same name but different parameters?

    a) Polymorphism
    b) Encapsulation
    c) Overloading
    d) Abstraction

33. Which SQL statement would you use to create an index on a table?

    a) ADD INDEX
    b) CREATE INDEX
    c) MAKE INDEX
    d) INSERT INDEX

34. What is the output of the following JavaScript code?

    ```javascript
    console.log(typeof typeof 1);
    ```

    a) "number"
    b) "string"
    c) "undefined"
    d) "object"

35. In a SQL database, what is a transaction?

    a) A unit of work that is performed against a database
    b) A type of join operation
    c) A method to create new tables
    d) A way to sort query results
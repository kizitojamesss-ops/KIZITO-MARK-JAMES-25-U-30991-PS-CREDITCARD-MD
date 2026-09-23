KIZITO-MARK-JAMES-25-U-30991-PS-CREDITCARD-MD

Overview

A credit card number is considered valid by this program if it meets three criteria:

1 Length Check:The total number of digits must be between 13 and 16.
2 Prefix Check:The number must start with a valid card brand prefix:
   4 — Visa
   5 — MasterCard
   37 — American Express
   6 — Discover
3 Luhn Checksum: The sum of doubled even-positioned digits (from right to left) plus the sum of odd-positioned digits must be divisible by 10 (total % 10 == 0).

 Function Breakdown
1 main()
 Reads the credit card number from standard input into a long long variable to prevent 32-bit integer overflow.
 Calls isValid(cardNumber) and outputs whether the number is valid or invalid.
2 isValid(long long number)
Acts as the main orchestrator for validation:
1 Calls getSize(number) to check if the length is between 13 and 16 digits.
2 Calls prefixMatched() to verify if the card starts with 4, 5, 37, or 6.
3 Calls sumOfDoubleEvenPlace() and sumOfOddPlace(), adds their results together, and checks if total % 10 == 0.
3 sumOfDoubleEvenPlace(long long number) & getDigit(int number)
Processes every second digit from right to left (starting with the 2nd to last digit):
Skips the last digit (number = number / 10).
Extracts the second-to-last digit (number % 10) and multiplies it by 2.
Calls getDigit() to process the doubled value:
If the doubled value is a single digit (e.g., 4 \times 2 = 8), it remains 8.
If the doubled value is two digits (e.g., 7 \times 2 = 14), getDigit() adds the digits together: 1 + 4 = 5.
Skips to the next pair (number = number / 10).
4 sumOfOddPlace(long long number)
Processes every odd-positioned digit from right to left (1st, 3rd, 5th, etc.):
Extracts the last digit (number % 10) and adds it directly to sum.
Truncates the last two digits (number = number / 100) to jump to the next odd position.
5 prefixMatched(long long number, int d) & getPrefix(long long number, int k)
Checks if number starts with a specific prefix d:
prefixMatched() calculates the number of digits in d (e.g., prefix 37 has size 2).
getPrefix() extracts the first k digits from the left side of the card number by repeatedly dividing by 10.
Compares the extracted prefix against d.
6 getSize(long long d)
A utility function that counts the number of digits in a long long integer by repeatedly dividing by 10 until it reaches 0.

Example
Given the card number 4388576018402626:
1 Double every second digit from right to left:
Digits at even places (from right): 2, 0, 8, 0, 7, 8, 8, 4
Multiply by 2: 4, 0, 16, 0, 14, 16, 16, 8
Sum single/summed digits via getDigit(): 4 + 0 + (1+6) + 0 + (1+4) + (1+6) + (1+6) + 8 = 37
2 Sum odd-positioned digits from right to left:
Digits at odd places: 6, 6, 4, 1, 6, 5, 3 (excluding prefix position)
Sum: 6 + 6 + 4 + 1 + 6 + 5 + 3 = 31
3 Total Sum:
37 + 31 = 68
Check: 68 (mod 10) = 8 != 0 Invalid Card Number

# Python Coding Interview Questions

I have put together a set of Python coding questions that are typically asked in interviews, drawing on my experience as both interviewer and interviewee. Some of these are questions I have been asked in actual interviews, some are questions from all over the web and I have provided my answers to them irrespective of whether it is the same as the source or not, and some I have simply thought up possible questions in an interview.

I have also create a set of interview tips and tricks for coding interviews, which will help avoid typical behavioral mistakes that candidates often make. [trade_transactions.csv](https://github.com/arindamsinha12/scripts/tree/main/data)

My strong suggestion is that anyone using this should try to solve the questions first before looking at the answers in an imaginary interview setting. Give yourself 10 minutes to solve each question.

#### 1. Given a number such as 7345437, determine if it is a palindrome or not in two ways (a) by converting it to string, (b) without converting it to string.

**Converting it to string:**

```
num = 7345437
if str(num) == str(num)[::-1]:
    print('Is a palindrome')
else:
    print('Is not a palindrome')
```

**Without converting to string:**

```
def check_palindrome (num, num_len):
    if num // 10 == 0:  # A single digit
        return True

    if num // 100 == 0:  # Two digits
        if num // 10 == num % 10:
            return True
        else:
            return False

    if num // (10 ** (num_len - 1)) != num % 10:
        return False
    else:
        num =  (num % (10 ** (num_len - 1))) // 10
        num_len = num_len - 2
        return check_palindrome(num, num_len)

num = 7345437
num_len = 1

while num // (10 ** num_len) > 0:
    num_len += 1

if check_palindrome(num, num_len):
    print('Is a palindrome')
else:
    print('Is not a palindrome')    
```


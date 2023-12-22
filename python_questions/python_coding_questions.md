# Python Coding Interview Questions

I have put together a set of Python coding questions that are typically asked in interviews, drawing on my experience as both interviewer and interviewee. Some of these are questions I have been asked in actual interviews, some are questions from all over the web and I have provided my answers to them irrespective of whether it is the same as the source or not, and some I have simply thought up possible questions in an interview.

I have also create a set of interview tips and tricks for coding interviews, which will help avoid typical behavioral mistakes that candidates often make. [trade_transactions.csv](https://github.com/arindamsinha12/scripts/tree/main/data)

My strong suggestion is that anyone using this should try to solve the questions first before looking at the answers in an imaginary interview setting. Give yourself 10 minutes to solve each question.

#### Q1)
Given a number such as 7345437, determine if it is a palindrome or not in two ways (a) by converting it to string, (b) without converting it to string.

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

#### Q2)
Charles and Peter are play rock-paper-scissors.
- Rock beats scissors
- Scissors beats paper
- Paper beats rock

If they both pick the same, it is a draw.

Write a function to determine the winner starting with the below code snippet:
Charles = "Rock"
Peter = "Paper"

**Solution:**

This can be done using a longish if...else, but using a dictionary is a more elegant solution.

```
Charles = "Rock"
Peter = "Paper"
win_dict = {"Scissors": {"Paper": 1, "Rock": 0},
            "Rock": {"Scissors": 1, "Paper": 0},
            "Paper": {"Rock": 1, "Scissors": 0}}

def get_winner(player1, player2, win_dict):
    if player1 == player2:
        return 10
    else:
        win = win_dict[player1][player2]
        if win == 1:
                return 0
        else:
                return 1

player_list = ["Charles", "Peter"]

result = get_winner(Charles, Peter, win_dict)

if result == 10:
    print("Draw")
else:
    print(f'{player_list[result]} wins')
```

#### Q3)
You are given a nested dictionary.

```
emp_dict = {'emp1': {'first_name': 'Robert', 'last_name': 'Long'},
            'emp2': {'first_name': 'Alice', 'last_name': 'Smith'},
            'emp3': {'first_name': 'Chen', 'last_name': 'Yung'}}
```

Given a dot separated path, get the corresponding value from the dictionary.

path = 'emp2.last_name'

**Iterative Solution:**

```
emp_dict = {'emp1': {'first_name': 'Robert', 'last_name': 'Long'},
            'emp2': {'first_name': 'Alice', 'last_name': 'Smith'},
            'emp3': {'first_name': 'Chen', 'last_name': 'Yung'}}

path = 'emp2.last_name'
path_list = path.split('.')

for pth in path_list:
    emp_dict = emp_dict[pth]

print(emp_dict)
```

**Recursive Solution:**

```
emp_dict = {'emp1': {'first_name': 'Robert', 'last_name': 'Long'},

            'emp2': {'first_name': 'Alice', 'last_name': 'Smith'},

            'emp3': {'first_name': 'Chen', 'last_name': 'Yung'}}

path = 'emp2.last_name'
path_list = path.split('.')

def get_value(path_list, emp_dict):
    if len(path_list) == 1:
        return emp_dict[path_list[0]]
    else:
        return get_value(path_list[1:], emp_dict[path_list[0]])

print(get_value(path_list, emp_dict))
```

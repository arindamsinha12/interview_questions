# Python Coding Interview Questions

I have put together a set of Python coding questions that are typically asked in interviews, drawing on my experience as both interviewer and interviewee. Some of these are questions I have been asked in actual interviews, some are questions from all over the web and I have provided my answers to them irrespective of whether it is the same as the source or not, and some I have simply thought up possible questions in an interview.

I have also create a set of [Coding interview Tips](https://github.com/arindamsinha12/interview_questions/blob/main/coding_interview_tips.md) for coding interviews, which will help avoid typical behavioral mistakes that candidates often make.

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
Charles and Peter are playing rock-paper-scissors.
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
emp_dict = {'emp1': {'first_name': 'Robert', 'last_name': 'Long'},  
            'emp2': {'first_name': 'Alice', 'last_name': 'Smith'},  
            'emp3': {'first_name': 'Chen', 'last_name': 'Yung'}}

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

#### Q4)

Insert the first string in the middle of the second string.  
first_string = "Something"  
second_string = "great"

```
first_string = "Something"
second_string = "great"

print(first_string[:len(first_string) // 2] + second_string + first_string[len(first_string) // 2:])
```

### Q5)

Find (a) all words that are in common to both sentences and, (b) all words that are not in common between both sentences.  
sent1 = "This is a test string for finding commonality"  
sent2 = "This string is the one for finding the answers"

```
sent1 = "This is a test string for finding commonality"
sent2 = "This string is the one for finding the answers"

sent1_set = set(sent1.split())
sent2_set = set(sent2.split())
print("Words in common - " + ", ".join(sent1_set & sent2_set))
print("Words not in common - " + ", ".join(sent1_set ^ sent2_set))
```

Note: Set operations - For two sets **seta** and **setb**:  
Difference: seta - setb  
Union: seta | set b  
Intersection: seta & setb  
Symmetric Difference: seta ^ setb

### Q6)

Find the most frequent character and it's count of occurences in the string "abracadabra".

```
strg = "abracadabra"
print(max({i:strg.count(i) for i in strg}.items(), key=lambda i:i[1]))
```

### Q7)

Find the string containing all unique characters in the string "abracadabra", in the order that it first occurs in the string.

```
input_string = 'abracadabra'
print("".join(sorted(set(input_string), key=input_string.index)))
```

### Q8)

Sort the dictionary (a) in the order of keys, (b) in the order of values and, (c) in the order of length of their keys.  
dict1 = {'two': 3, 'one': 5, 'three': 2, 'four': 4}

```
dict1 = {'two': 3, 'one': 5, 'three': 2, 'four': 4}

print("By key:", dict(sorted(dict1.items())))
print("By value:", dict(sorted(dict1.items(), key=lambda i: i[1])))
print("By key length:", dict(sorted(dict1.items(), key=lambda i: len(i[0]))))
```

### Q8)

Count the number of occurences of each word in the sentence "This is a test of a string to test a word count".

```
words = "This is a test of a string test a word count".split()
word_count = {i:words.count(i) for i in words}
print(word_count)
```

### Q9)

Find the maximum value in a list in (a) ASCII order and (b) word length.  
words = \['This', 'is', 'a', 'test', 'of', 'a', 'string', 'test', 'a', 'word', 'count']

```
words = ['This', 'is', 'a', 'test', 'of', 'a', 'string', 'test', 'a', 'word', 'count']
print("ASCII order:", max(words))
print("By length:", max(words, key=len))
```

### Q10)

Find the maximum value of in a dictionary (as a tuple (key, value)) (a) by key, (b) by max value length, and (c) by value.  
dict1 = {'one': 'fifteen', 'two': 'sixteen', 'five': 'eleven', 'three': 'twelve', 'four': 'thirteen'}

```
Max by key:
print(max(dict1.items()))

Max by value length:
print(max(dict1.items(), key=lambda x: len(x[1])))

Max by value:
print(max(dict1.items(), key=lambda x: x[1]))
```

### Q11)

Find the common characters between two strings 'broad' and 'abracadabra' in (a) any order, and (b) in the order in which they first appear in 'abracadabra'.

```
In any order:
"".join(set('broad') & set('abracadabra'))
```

### Q12)

Find the count of characters in string 'abracadabra' as a list of tuple(char, count), with characters in decreasing order of frequency.

```
input_string = 'abracadabra'
char_count = {i:list(input_string).count(i) for i in input_string}
print(sorted(char_count.items(), key=lambda x: x[1], reverse=True))
```

### Q12)

Find longest common prefix in a list of strings.  
Example strings:  
input_list = \['manage', 'mango', 'man', 'manifest']  
input_list = \['manage', 'mango', 'many', 'manifest']

```
common_prefix = ''
min_len = len(min(input_list, key=len))
for i in range(min_len):
    prefix_set = set(map(lambda x: x[:i+1], input_list))
    if len(prefix_set) == 1:
        common_prefix = prefix_set.pop()
    else:
        break
		
print(common_prefix)
```

### Q13)

List of all combinations of 0..x, 0..y, 0..z where the sum of the components of any combination (x, y, z) does not add up to 4.  
x = 2, y = 3, z = 4  
n = 4

```
x = 2
y = 3
z = 4
n = 4
[[a, b, c] for a in range(x + 1) for b in range(y + 1) for c in range(z + 1) if a+b+c != n]
```

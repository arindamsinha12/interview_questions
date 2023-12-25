# SQL Coding Interview Questions

I have put together a set of Python coding questions that are typically asked in interviews, drawing on my experience as both interviewer and interviewee. Some of these are questions I have been asked in actual interviews, some are questions from all over the web and I have provided my answers to them irrespective of whether it is the same as the source or not, and some I have simply thought up possible questions in an interview.

I have also create a set of [Coding interview Tips](https://github.com/arindamsinha12/interview_questions/blob/main/coding_interview_tips.md) for coding interviews, which will help avoid typical behavioral mistakes that candidates often make.

My strong suggestion is that anyone using this should try to solve the questions first before looking at the answers in an imaginary interview setting. Give yourself 10 minutes to solve each question.

#### Q1)

A teacher wants to shuffle their students in such a way, that each student in an odd numbered position moves back one seat and each in an even numbered position moves forward one seat. If the last student is in an odd numbered position, leave that unchanged. Based on the same table **students** below, write and SQL to do the same.

Table **students**:  
|Position|Name|  
+-------------+  
|1| Alice          |  
+----------+----------------+  
|      2   | Ramesh         |  
+----------+----------------+  
|      3   | Chan           |  
+----------+----------------+  
|      4   | John           |  
+----------+----------------+  
|      5   | Rita           |  
+----------+----------------+

Result required:  
|Position|Name|  
+-------------+  
|      1   | Ramesh         |  
+----------+----------------+  
|      2   | Alice          |  
+----------+----------------+  
|      3   | John           |  
+----------+----------------+  
|      4   | Chan           |  
+----------+----------------+  
|      5   | Rita           |  
+----------+----------------+

```
SELECT CASE WHEN position = (SELECT MAX(position) FROM students) AND position % 2 = 1 THEN position
            WHEN position % 2 = 1 THEN position + 1
            ELSE position - 1
       END AS position,
       name
FROM students
ORDER BY position;
```

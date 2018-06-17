# Problem
https://www.hackerrank.com/challenges/grading/problem
```
학생들의 점수(0~100)가 배열의 형태로 주어질 때, 각 점수를 올림해줄 수 있으면 올려주도록 하라.
'올림' 하는 기준은, 올린 점수와 원 점수의 차이가 3 미만이고, 올린 점수가 40점 이상이어야 한다. 조건에 해당하지 않으면 원 점수 그대로.
```

# Solution
```java
int[] gradingStudents(int[] grades) {
    for(int i = 0; i < grades.length; ++i) {
        int grade = grades[i];
        if (grade % 5 != 0) {
            int newGrade = (grade / 5 + 1) * 5;
            if (newGrade >= 40 && (newGrade - grade < 3)) {
                grades[i] = newGrade;
            }
        }
    }
    return grades;
}
```
Time complexity: O(n)<br/>
Space complexity: O(1)

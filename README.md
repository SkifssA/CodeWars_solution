# CodeWars_solution
Решение задач на языке программирования Python. Тренажер [codewars.com](https://www.codewars.com/kata/latest/my-languages?beta=false)


`Matrix Determinant`
[Задача](https://www.codewars.com/kata/52a382ee44408cea2500074c)
```python
import copy
def determinant(n: list):
    if len(n) == 1:
        return n[0][0]
    if len(n) == 2:
        return n[0][0] * n[1][1] - n[1][0] * n[0][1]
    res = 0
    for i in range(len(n)):
        w = copy.deepcopy(n)[1:]
        for j in range(len(w)):
            w[j].pop(i)
        res += n[0][i] * determinant(w) * ((-1) ** i)
    return res
```

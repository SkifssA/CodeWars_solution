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
`Brainfuck Translator`
[Задача](https://www.codewars.com/kata/58924f2ca8c628f21a0001a1)
```python
import re
def brainfuck_to_c(string: str):
    string_old = string
    comand_C = {'+': lambda x: f'*p += {x};\n',
                '-': lambda x: f'*p -= {x};\n',
                '<': lambda x: f'p -= {x};\n',
                '>': lambda x: f'p += {x};\n',
                '.': 'putchar(*p);\n',
                ',': '*p = getchar();\n',
                '[': 'if (*p) do {\n',
                ']': '} while (*p);\n'}

    string = re.sub('[^+\-,.<>\[\]]', '', string_old)

    string = string.replace('+-', '').replace('<>', '').replace('[]', '').replace('-+', '').replace('><', '')
    while string != string_old:
        string_old = string
        string = string.replace('+-', '').replace('<>', '').replace('[]', '').replace('-+', '').replace('><', '')
    d = 0
    string = re.sub('[^\[\]]', '', string_old)
    for i in string:
        if i == '[':
            d += 1
        elif i == ']':
            d -= 1
        if d < 0:
            return "Error!"
    else:
        if d != 0:
            return "Error!"

    string = ''
    space = 0
    while len(string_old) != 0:
        w = string_old[0]
        if w in '+-<>':
            q = re.search(f'[{w}]+', string_old)[0]
            string_old = string_old.replace(q, '', 1)
            string += (' ' * space) + comand_C[w](len(q))
        elif w in '.,[]':
            if w == ']':
                space -= 2
            string_old = string_old[1:]
            string += (' ' * space) + comand_C[w]
            if w == '[':
                space += 2
    return string
```

`Sort binary tree by levels`
[Задача](https://www.codewars.com/kata/52bef5e3588c56132c0003bc)
```python
def tree_by_levels(s):
    if not s:
        return []
    o = []
    d = [s]
    while d != []:
        for i in d.copy():
            o.append(i.value)
            if i.left != None:
                d.append(i.left)
            if i.right != None:
                d.append(i.right)
            d.pop(0)
        
    return o
```

`Text align justify`
[Задача](https://www.codewars.com/kata/537e18b6147aa838f600001b)
```python
def justify(text, width):
    text = text.split()
    string = ''
    while not len(text) == 0:
        s = [0,0]
        for i in text:
            s[0] += len(i) + 1
            s[1] += 1
            if s[0] >= width:
                if s[0]-1 > width:
                    s[0]-=len(i) + 1
                    s[1] -= 1
                n = 0
                for j in range(s[1]):
                    n += len(text[j])
                n = width - n
                if s[1] - 1 != 0:
                    r = [1 for i in range(s[1] - 1)]
                    kos = 0
                    while not sum(r) >= n:
                        r[kos]+= 1
                        kos += 1
                        if kos == len(r):
                            kos = 0 
                string += text[0]
                text = text[1:]
                for q in range(s[1]-1):
                    string+= ' ' * r[q] + text[0]
                    text = text[1:]
                string += '\n'
                break
            elif i == text[-1]:
                string += ' '.join(text)
                text = []
                break
    return string if string[-1]!='\n' else string[:-1]
```

`Rail Fence Cipher: Encoding and Decoding`
[Задача](https://www.codewars.com/kata/58c5577d61aefcf3ff000081)
```python
def encode_rail_fence_cipher(string, n):
    a = [[] for i in range(n)]
    i = 1
    q = 0
    while not string == '':
        a[q].append(string[0])
        string = string[1:]
        q += i
        if q == -1 or q == n:
            i *= -1
            q += i*2
    string = ''
    for s in a:
        print(s)
        string += ''.join(s)
    return string
    
def decode_rail_fence_cipher(string, n):
    print(string, n)
    print(len(string))
    a = [[] for i in range(n)]
    temp = string
    s = [len(string)//(n+n-2),len(string)%(n+n-2)]
    print(s)
    for i in range(n):
        q = (s[0] * ((i>0 and i<n-1)+1))+(s[1]>i)+(s[1]>n+n-2-i)
        print(q)
        a[i] = string[:q]
        string = string[q:]
    s = ''
    i = 1
    q = 0
    print(a)
    while not len(temp) == len(s):
        s += a[q][:1]
        a[q] = a[q][1:]
        q += i
        if q == -1 or q == n:
            i *= -1
            q += i*2
    return s
```

`Pete, the baker`
[Задача](https://www.codewars.com/kata/525c65e51bf619685c000059)
```python
cakes = lambda r, a:min([a[i]//r[i] if i in a else 0 for i in r])
```

`RGB To Hex Conversion`
[Задача](https://www.codewars.com/kata/513e08acc600c94f01000001)
```python
def rgb(r, g, b):
    r = 0 if r<0 else r if r<255 else 255
    b = 0 if b<0 else b if b<255 else 255
    g = 0 if g<0 else g if g<255 else 255
    return "{:02X}{:02X}{:02X}".format(r,g,b)
```

`int32 to IPv4`
[Задача](https://www.codewars.com/kata/52e88b39ffb6ac53a400022e)
```python
int32_to_ip = lambda int32: '.'.join([str(int((b:= b if len(b:= bin(int32)[2:])==32 else '0'*(32-len(b))+b)[8*x:8*(x+1)],2)) for x in range(4)])
```

`Luck check`
[Задача](https://www.codewars.com/kata/5314b3c6bb244a48ab00076c)
```python
def luck_check(string):
    int(string)
    x = len(string)//2
    w = [string[:x], string[x:]] if len(string)%2 == 0 else [string[:x], string[x+1:]]
    n,b = 0,0
    for i in range(len(w[0])):
        n+=int(w[0][i])
        b+=int(w[1][i])
    return n == b
```

`Memoized Log Cutting`
[Задача](https://www.codewars.com/kata/54b058ce56f22dc6fe0011df)
```python
def cut_log(p, n):
    for i in range(2, n + 1):
        p[i] = max(p[i-k] + p[k] for k in range((i//2)+1))
    return p[n]
```

`Human readable duration format`
[Задача](https://www.codewars.com/kata/52742f58faf5485cae000b9a)
```python
def format_duration(seconds):
    if seconds == 0: return 'now'
    str_ = []
    w,x,s = [1,60,60,24,365,999],1, ['second', 'minute', 'hour', 'day', 'year']
    for i in range(len(w)-1):
        x *= w[i]
        n = (seconds//x)%(w[i+1])
        if n != 0:
            str_.append(str(n) + ' ' + s[i]+('s' if n > 1 else ''))
    str_.reverse()
    if len(str_) > 1:
        str_ = ', '.join(str_[:-1])+' and '+str_[-1]
    else:
        str_=str_[-1]
    return(str_)
```

`Range Extraction`
[Задача](https://www.codewars.com/kata/51ba717bb08c1cd60f00002f)
```python
def solution(args):
    str_, e = [], []
    b, n = 0, 0
    for i in range(len(args)-1):
        if args[i]+1 == args[i+1]:
            n = i+1
        else:
            str_.append([args[b], args[n]])
            n = i+1
            b = i+1
    str_.append([args[b], args[n]])
    for x in str_:
        if x[0] == x[1]:
            e.append(str(x[0]))
        elif x[0]+1 == x[1]:
            e.append(str(x[0]))
            e.append(str(x[1]))
        else:
            e.append(str(x[0])+'-'+str(x[1]))
    return(','.join(e))
```

`Lazy Repeater`
[Задача](https://www.codewars.com/kata/51fc3beb41ecc97ee20000c3)
```python
def make_looper(string):
    i = -1
    def a():
        nonlocal i
        i+=1
        return string[i%len(string)]
    return a
```

`First non-repeating character`
[Задача](https://www.codewars.com/kata/52bc74d4ac05d0945d00054e)
```python
def first_non_repeating_letter(string):
    for i,x in enumerate(string.lower()):
        if string.lower().count(x) == 1:
            return string[i]
    return ''
```

`Ninja vs Samurai: Attack + Block`
[Задача](https://www.codewars.com/kata/517b2bcf8557c200b8000015)
```python
Position = {'high': 'h', 'low': 'l'}

class Warrior():
    def __init__(self, name):
        self.name = name
        self.health = 100
        self.block = ""
        self.deceased = False
        self.zombie = False
        
    def attack(self, enemy, position):
        damage = 0
        if enemy.block != position: damage += 10 if position == Position['high'] else 5
        if enemy.block == "": damage += 5
        enemy.set_health(enemy.health - damage)
    
    def set_health(self, new_health):
        self.health = max(0, new_health)
        if self.deceased: self.zombie = True
        if self.health == 0 and not self.deceased:
            self.deceased = True
            self.zombie = False
```

`A Chain adding function`
[Задача](https://www.codewars.com/kata/539a0e4d85e3425cb0000a88)
```python
class add(int):
    def __call__(self, n):
        return add(self + n)
```

`Scramblies`
[Задача](https://www.codewars.com/kata/55c04b4cc56a697bb0000048)
```python
def scramble(s1, s2):
    s1, s2 = list(s1), list(s2)
    for i in set(s2):
        if s2.count(i) > s1.count(i):
            return False
    return True
```

`Decimal to Factorial and Back`
[Задача](https://www.codewars.com/kata/54e320dcebe1e583250008fd)
```python
def fac(n):
    for x in range(1,n):
        n*=x
    return n

def dec_2_fact_string(nb):
    w,s,d = [],36,False
    while s!=0:
        if str(nb//fac(s))=='0' and not d:
            s-=1  
            continue
        if str(nb//fac(s))!='0':
            d = True
        q = nb//fac(s)
        w.append(str(q) if q<10 else chr(q+ord('A')-10))
        nb-=q*fac(s)
        s-=1
    return ''.join(w)+'0'

def fact_string_2_dec(string):
    n = 0
    for i in range(len(string)):
        n+=(((int(string[i]) if ord(string[i])>=48 and ord(string[i])<=58 else (ord(string[i])-ord('A')+10))*fac(len(string)-i-1)))
    return n
```

`Decode the Morse code, advanced`
[Задача](https://www.codewars.com/kata/54b72c16cd7f5154e9000457)
```python
def decode_bits(bits):
    import re
    bits = bits.strip('0')
    time_unit = min(len(m) for m in re.findall(r'1+|0+', bits))
    return bits[::time_unit].replace('111', '-').replace('1','.').replace('0000000','   ').replace('000',' ').replace('0','')

def decode_morse(mc):
    return ' '.join(''.join([MORSE_CODE[i] if i != '' else ' ' for i in mc.split(' ')]).split())
```

`Sum by Factors`
[Задача](https://www.codewars.com/kata/54d496788776e49e6b00052f)
```python
def factorization(n):
    p = []
    d = 2
    while d * d <= n:
        while n % d == 0:
            p.append(d)
            n //= d
        d += 1
    if n > 1:
        if n not in p :
            p.append(n)
    return p

def sum_for_list(lst):
    print(lst)
    arr = [list(set(factorization(abs(i)))) for i in lst]
    a,n,r = [],0,[]
    for x in arr:
        a += x
    a = sorted(set(a))
    for x in a:
        for i in range(len(arr)):
            if arr[i].count(x)!=0:
                n += lst[i]
                print(lst[i], x)
        r.append([x,n])
        n = 0
    return r
```

`Strip Comments`
[Задача](https://www.codewars.com/kata/51c8e37cee245da6b40000bd)
```python
def strip_comments(strng, markers):
    r = [x for x in strng.split('\n')]
    h, z = [], True
    w = []
    for x in r:
        for e in markers:
            if x.count(e)!=0:
                w.append(x.index(e))
        if w != []:
            l = min(w)
            h.append(x[:l if x[l-1]!=' ' and x[l-1]!='\t' else l-1])
            z = False
        if z: 
            h.append(x)
        z = True;
        w = []
    return '\n'.join(h) if h[0] != ' ' else '\n' +'\n'.join(h[1:])
```

`Tic-Tac-Toe Checker`
[Задача](https://www.codewars.com/kata/525caa5c1bf619d28c000335)
```python
def is_solved(board):
    x, o, r = 0, 0, False
    for i in range(6):
        for j in range(3):
            if i <3:
                if board[i%3][j] != 0:
                    if board[i%3][j] == 1: x +=1
                    else: o += 1
                else: r = True
            else:
                if board[j][i%3] != 0:
                    if board[j][i%3] == 1: x +=1
                    else: o += 1
        if x == 3 or o == 3:
            return 1 if x == 3 else 2
        o, x = 0, 0
    if  (board[0][0] == board[1][1] and board[0][0] == board[2][2] and board[1][1] != 0) or \
        (board[2][0] == board[1][1] and board[0][2] == board[1][1] and board[1][1] != 0):
        return board[1][1]
    return -1 if r else 0
```

`Smallest possible sum`
[Задача](https://www.codewars.com/kata/52f677797c461daaf7000740)
```python
def solution(a):
    while 1:
        a.sort()
        if a[-1] == a[0]:
            return a[0]*len(a)
        a = [[a[0],x%a[0]][bool(x%a[0])] for x in a]
```

`Vigenère Cipher Helper`
[Задача](https://www.codewars.com/kata/52d1bd3694d26f8d6e0000d3)
```python
class VigenereCipher(object):
    def __init__(self, key, alphabet):
        self.key = key
        self.alp = alphabet
    
    def encode(self, text):
        print()
        return ''.join([self.alp[(self.alp.find(text[i]) + self.alp.find(self.key[i%len(self.key)]))%len(self.alp)]\
                        if self.alp.find(text[i]) != -1 else text[i]\
                        for i in range(len(text))])
    
    def decode(self, text):
        return ''.join([self.alp[(self.alp.find(text[i]) - self.alp.find(self.key[i%len(self.key)]))%len(self.alp)]\
                        if self.alp.find(text[i]) != -1 else text[i]\
                        for i in range(len(text))])
```

`Snail`
[Задача](https://www.codewars.com/kata/521c2db8ddc89b9b7a0000c1)
```python
def snail(map):
    dx, dy = 1, 0
    x, y = 0, 0
    arr = []
    n = len(map)
    if len(map[0]) == 0: return []
    print(map,n)
    for i in range(n**2):
        arr.append(map[y][x])
        map[y][x] = False
        nx, ny = x+dx, y+dy
        if 0 <= nx < n and 0 <= ny < n and map[ny][nx]:
            x, y = nx, ny
        else:
            dx, dy = -dy, dx
            x, y = x+dx, y+dy
    return arr
```

`Moving Zeros To The End`
[Задача](https://www.codewars.com/kata/52597aa56021e91c93000cb0)
```python
def move_zeros(lst):
    return [x for x in lst if x != 0]+([0 for i  in range(lst.count(0))])
```

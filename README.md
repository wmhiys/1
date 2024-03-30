# 1
def book_count(alist):
    ''' Описание функции:
    функция для подсчета количества книг пор темам
    res - словарб, чтобы обращаться к количеству в нем книг'''
    res = {}
    for i in range(len(alist)):
        if len(alist[i][4])>0:
            if alist[i][1] not in res:
                res[alist[i][1]] = int(alist[i][4])
            else:
                res[alist[i][1]] += int(alist[i][4])
    return res


def report(alist):
    '''Описание функции:
    функция для создания строк о данных темах и количества в ней книг
    '''
    with open('count_book.txt', 'w', encoding='utf8') as f:
        for keys in alist:
            f.write(f'Книг для изучения {keys} в библиотеке нашлось: {alist[keys]}\n')


with open('languages.csv', encoding='utf8') as f:
    name = f.readline()
    n = f.readlines()
for i in range(len(n)):
    if i != len(n) - 1:
        n[i] = n[i][:-1]
        n[i] = n[i].split(';')
    else:
        n[i] = n[i].split(';')
res = book_count(n)
report(res)
#2
def quicksort(alist, start, end):
    if end - start > 1:
        p = partition(alist, start, end)
        quicksort(alist, start, p)
        quicksort(alist, p + 1, end)


def partition(alist, start, end):
    pivot = alist[start]
    i = start + 1
    j = end - 1

    while True:
        while (i <= j and alist[i] <= pivot):
            i = i + 1
        while (i <= j and alist[j] >= pivot):
            j = j - 1

        if i <= j:
            alist[i], alist[j] = alist[j], alist[i]
        else:
            alist[start], alist[j] = alist[j], alist[start]
            return j


best=[]
prom = []
with open('languages.csv', encoding='utf8') as f:
    name = f.readline()
    n = f.readlines()
for i in range(len(n)):
    if i != len(n) - 1:
        n[i] = n[i][:-1]
        n[i] = n[i].split(';')
        prom.append(n[i][0])
    else:
        n[i] = n[i].split(';')


quicksort(prom,0,len(prom))
for i in range(len(prom)):
    x=0
    while prom[i] not in n[x]:
        x+=1
    best.append(n[x])


print(f'{best[0][2]}:')
for j in range(2):
    print(f'\t{best[j][0]} - {best[j][3]}')
print(f'{best[2][2]}:')
print(f'\t{best[2][0]} - {best[2][3]}')
#3
def message_send(alist):
    '''Описание функции:
    функция для создания строки сообщения с данными значениями
    '''
    return f'{alist[0]} был создан: {alist[3]} в {alist[2]}'


best = []
with open('languages.csv', encoding='utf8') as f:
    name = f.readline()
    n = f.readlines()
for i in range(len(n)):
    if i != len(n) - 1:
        n[i] = n[i][:-1]
        n[i] = n[i].split(';')
        best.append(n[i][0])
    else:
        n[i] = n[i].split(';')
        best.append(n[i][0])
message = input()
while message != 'stop':
    if message not in best:
        print('Хм.. Вы уверены, что слышали об этом ЯП?')
        message = input()
    else:
        ind = best.index(message)
        print(message_send(n[ind]))
        message = input()
#4
def result(alist):
    '''Описание функции:
    функция для создания рейтинга данных языков программирования'''
    return [alist[0],int(alist[-1])/(2023-int(alist[2]))]


with open('languages.csv', encoding='utf8') as f:
    name = f.readline()
    n = f.readlines()
for i in range(len(n)):
    if i != len(n) - 1:
        n[i] = n[i][:-1]
        n[i] = n[i].split(';')
    else:
        n[i] = n[i].split(';')

for i in range(len(n)):
    if i != len(n)-1:
        print(*result(n[i]))


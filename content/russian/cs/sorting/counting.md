---
title: Сортировка подсчетом
weight: 8
---

Все предыдущие алгоритмы работали с массивами, в которых лежат могут лежать абсолютно любые объекты, которые можно сравнивать: числа, строки, пары, другие массивы — почти все что угодно.

В особом случае, когда элементы могут принадлежать только какому-то небольшому множеству, можно использовать другой алгоритм — *сортировку подсчетом* (англ. *counting sort*).

Пусть, например, нам гарантируется, что все числа натуральные и лежат в промежутке от $1$ до $100$. Тогда есть такой простой алгоритм:

- Создадим массив размера $100$, в котором будем хранить на $k$-ом месте, сколько раз число $k$ встретилось в этом массиве.
- Пройдемся по всем числам исходного массива и увеличим соответствующее значение массива на $1$.
- После того, как мы посчитали, сколько раз каждое число встретилось, можно просто пройтись по этому массиву и вывести $1$ столько раз, сколько встретилась $1$, вывести $2$ столько раз, сколько встретилась $2$, и так далее.

Время работы такого алгоритма составляет $O(m + n)$, где $m$ — число возможных значений, $n$ — число элементов в массиве. Если количество возможных различных элементов в множестве относительно невелико, то сортировка подсчетом является одним из самых оптимальных решений.

### Вариант реализации

Создадим массив $c$ размера $100$ и заполним его, один раз пройдясь по исходному массиву.

Затем заведем указатель $k$ на позицию в исходном массиве, куда нужно записывать очередное число, и будем увеличивать его каждый раз, когда мы уменьшаем очередную ячейку в $c$.

```cpp
void count_sort(int *a, int n) {
    int c[100] = {0};

    for (int i = 0; i < n; i++)
        c[a[i]]++;

    int k = 0;
    for (int i = 0; i < 100; i++)
        while (c[i]--)
            a[k++] = i;
}
```
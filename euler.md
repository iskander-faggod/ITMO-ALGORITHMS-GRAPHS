``` cpp
procedure find_all_cycles (v)
 var массив cycles 1.
   пока есть цикл, проходящий через v,
   находим его добавляем все вершины найденного цикла в
   массив cycles (сохраняя порядок обхода)
   удаляем цикл из графа 2.
   
   идем по элементам массива cycles каждый элемент cycles[i]
   добавляем к ответу из каждого элемента рекурсивно 
   вызываем себя: find_all_cycles (cycles[i])
```

Теперь мы будем решать задачу нахождения цикла в предположении, что он точно есть. Давайте запустимся из произвольной вершины, пройдем по любому ребру и удалим его.

```cpp
void euler(int v){
    stack >s;
    s.push({v, -1});
    while (!s.empty()) {
        v = s.top().first;
        int x = s.top().second;
        for (int i = 0; i < g[v].size(); i++){
            pair e = g[v][i];
            if(!u[e.second]){
                u[e.second]=1;
                s.push(e);
                break;
            }
        }
        if (v == s.top().first) {
            if (~x) {
                p.push_back(x);
            }
            s.pop();
        }
    }
}
```
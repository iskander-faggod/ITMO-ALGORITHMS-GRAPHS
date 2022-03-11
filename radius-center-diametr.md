## Диаметр

```cpp
int Diam()
{
    int **edge = new int *[n];
    for (int i = 0; i < n; i++)
        edge[i] = new int [n];
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++) {
            edge[i][j] = a[i][j];
            if (!edge[i][j]) 
                edge[i][j] = 10000;
        }
    }
    for (int k = 0; k < n; k++)
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (i != j)
                    edge[i][j] = MIN(edge[i][j], edge[i][k]+edge[k][j]);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (edge[i][j] == 10000) 
                edge[i][j] = 0;
        }
    }
    int max = edge[0][1];
    for(int i = 0; i < n; i++)
    {
        for (int j = i+1; j < n; j++) {
            if(edge[i][j] > max)
                max = edge[i][j];
        }
    }
    return max;
    delete [] edge;
}
```

## Радиус

```cpp
int Radius(int f)
{
    int **edge = new int *[n];
    for (int i = 0; i < n; i++)
        edge[i] = new int [n];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            edge[i][j] = a[i][j];
            if (!edge[i][j]) 
                edge[i][j] = 10000;
        }
        for (int k = 0; k < n; k++)
            for (int i = 0; i < n; i++)
                for (int j = 0; j < n; j++)
                    if (i != j)
                        edge[i][j] = MIN(edge[i][j], edge[i][k]+edge[k][j]);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (edge[i][j] == 10000) 
                    edge[i][j] = 0;
            }
        }
        int min = edge[f][f+1];
        for (int j = f+1; j < n; j++) {
            if(edge[f][j] < min)
                min = edge[f][j];
        }
        return min;
        delete [] edge;
}
```

## Центр

```cpp
void Centr()
{
    int **edge = new int *[n];
    for (int i = 0; i < n; i++)
        edge[i] = new int [n];
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            edge[i][j] = a[i][j];
            if (!edge[i][j]) 
                edge[i][j] = 10000;
        }
        for (int k = 0; k < n; k++)
            for (int i = 0; i < n; i++)
                for (int j = 0; j < n; j++)
                    if (i != j)
                        edge[i][j] = MIN(edge[i][j], edge[i][k]+edge[k][j]);
        cout << "Расстояния: \n" << endl;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (edge[i][j] == 10000) 
                    edge[i][j] = 0;
                cout << edge[i][j] << " ";
            }
            cout << endl;
        }
        int min, max;
        int *ecc = new int [n];
        int *rad = new int [n];
        int *deg = new int [n];
        for (int i = 0; i < n; i++) {
            rad[i] = ecc[i] = deg[i] = 0;
            min = edge[i][i+1];
            max = edge[i][i+1];
            for (int j = i+1; j < n; j++) {
                if(edge[i][j] < min)
                {
                    min = edge[i][j];
                }
                if(edge[i][j] > max)
                    max = edge[i][j];
            }
            deg[i] = min;
            ecc[i] = max;
        }
        int j = 0;
        for(int i = 0; i < n; i++)
        {
            if(deg[i] == ecc[i])
                rad[j++] = i;
        }
        cout << "\n";
        cout << "Центры графа: ";
        for(int i = 0; i < j; i++)
            cout << rad[i]+1 << " ";
        delete [] edge;
        delete [] deg;
        delete [] rad;
        delete [] ecc;
}
```
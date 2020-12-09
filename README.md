# 29. Добавить ребро между заданными вершинами и в модифицированном графе найти вершину с минимальной степенью.

## Алгоритм:
- Увеличение размера массива для дополнительной строки матрицы инцидентности, заполнение новой строки соответствующими данными.
``` C
	++edge
    arr = realloc(arr, (point*edge)*sizeof(int));
	for(i = point*(edge - 1); i < point*edge; i++){
        if(first == i + 1 - point*(edge - 1)){
        	++check;
        	arr[i] = 1;
		}
		else if(second == i + 1 - point*(edge - 1)){
            ++check;
        	arr[i] = 1;
		}
		else{
			arr[i] = 0;
		}
	}
```
- Определение степени каждой вершины путём счёта инцидентных вершине рёбер.
``` C
	vert = (int *)calloc(point, sizeof(int));
	check = -1;
	for(i = 0; i < point; i++){
        for(j = 0; j < edge*point; j += point){
           	vert[i] += arr[i + j];
        }
	}
```
- Проверка наличия в графе петель и в случае их нахождения увеличение степени соответствующей вершины.
``` C
	for(i = 0; i < edge; i++){
		for(j = 0; j < point; j++){
			if(check != -1 && arr[i*point + j] == 1){
				check = -1;
			}
			else if(arr[i*point + j] == 1){
				check = j;
			}
		}
		if(check != -1){
			++vert[check];
			check = -1;	
		}
	}
```
- Нахождение минимальной степени вершины и вывод всей вершин с этой степенью.
``` C
	check = 1000;
    for(i = 0; i < point; i++){
    	if(check > vert[i]){
           	check = vert[i];
		}
	}
	for(i = 0; i < point; i++){
		if(vert[i] == check){
			printf("%d\n", i+1);
		}
	}
	printf("\n");
    free(vert);
```

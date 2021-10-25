## Оптимизации циклов (продолжение)

### Разбиение (fission) и объединение циклов
```
for(i) {
    A[i] = ...;
    B[i] = ...;
}
```
fission операция может выполняться в обе стороны
```
for(i) {
    A[i] = ...;
}
for(i) {
    B[i] = ...;
}
```
Объединение необходимо для ускорения, в случае простых операций в каждой итерации
Однако, если код действительно большой и не помещается в кеш используют Разбиение

### Перестановка циклов (interchange / permutation)
```
for(i) {
    for(j) {
        ...
    }
}
```
interchange ->
```
for(j) {
    for(i) {
        ...
    }
}
```
Используется при неэффективном обходе структур циклом, приводящем к промахам в кеш данных

### Разбиение цикла на блоки (loop tiling)
```
for(i) {
    for(j) {
        ...
    }
}
```
Переходит в цикл вложенности 4 или более в зависимости от того, на сколько разбита таблица данных

```
for(i) {
    for(j) {
        for(ii) {
            for(jj) {
                ...
            }
        }
    }
}
```

# Псевдонимы (Alias)

Указатели на одну и ту же область памяти
```
int k;
int *A;
int *B;
char *C;

<!-- Псевдонимы (habr/114117) -->

A = &k;
B = &k;
C = (char*)&k;
```
ключевое слово restrict

есть специальный режим для оценки aliases
- type-based alias analysis
- strict aliasing
на одну и ту же область памяти не могут указывать два указателя существенно разных типов
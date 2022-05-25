# Task #5: Programación concurrente  
**course:** Programación III  
**unit:** 5  
**cmake project:** prog3_programacion_concurrente_v2022_1
## Instructions
Subir a gradescope los siguientes archivos:
- `P1.h`
- `P2.h`
- `P3.h`
- `P4.h`

## Question #1 - Suma concurrente (4 points)

Implementar una función **`sumar`** que utilizando concurrencia realice la suma de todo los valores numericos de un
contenedor secuencial. Generalizar el programa para que acepte cualquier tipo de contenedor secuencial.
```cpp
template <typename T, template <typename...> class Container>
T sumar(Container<T>& cnt);
```
**Casos de uso**
```cpp
    size_t n = 0;
    cin >> n;
    vector<long long> v1(n);
    for (auto &item: v1)
        cin >> item;
    auto total = sumar(v1);
    cout << total << endl;
```

## Question #2 - Incremento Concurrente (4 points)

Implementar una función **`increase_values`** que utilizando concurrencia realice incremente todos los valores de un vector en
un valor dado. Generalizar el programa para que acepte cualquier tipo de contenedor secuencial.
```cpp
template<typename T, template<typename ...> class Container>
void increase_values(Container<T>& cnt, T value);
```
**Casos de uso**
```cpp
    size_t n = 0;
    int value = 0;
    cin >> n;
    cin >> value;
    vector<int> v1(n);
    for (auto &item: v1)
        cin >> item;
    increase_values(v1, value);
    auto current = begin(v1);
    cout << *current++;
    while(current != end(v1))
        cout << " " << *current++;
    cout << endl;
```

## Question #3 - Buscar números primos (4 points)

Elaborar la función **`get_primes`** que utilizando concurrencia genere una colección de números primos entre **`start`** y **`stop`** (sin incluir `stop`) y que los
almacene en un contenedor. El programa deberá asegurarse que los números sean almacenados en orden.
```cpp
template <typename T, template<typename ...> class Container>
void get_primes(Container<T>& cnt, T start, T stop);
```
**Casos de uso**
```cpp
    int first = 0;
    int last = 0;
    cin >> first >> last;
    vector<int> primes;
    get_primes(primes, first, last);
    auto current = begin(primes);
    cout << *current++;
    while(current != end(primes))
        cout << " " << *current++;
    cout << endl;
```

## Question #4 - single link list thread-safe (8 points)

Desarrollar el template de clase `linked_list_t` que se comporte como una lista simplemente enlazada, que permita insertar y borrar elementos al inicio de forma concurrente y que cuenten con los siguientes métodos:

- `push_front(const T& value)` permite agregar nuevos valores al inicio de la lista del tipo `T`.
- `pop_front()` permite borrar un valor al inicio de la lista.
- `bool empty()` retorna `true` si la lista esta vacía.
- `int size()` retorne la cantidad de datos grabados en la lista.
- `begin()` que retorne el iterador que tenga la referencia del primer elemento de la lista
- `end()` que retorne el iterador que tenga la referencia del valor siguiente al último.
Como se observa debera desarrollarse un forward iterador que de soporte a la lista simplemente enlazada, para lo cual debe cumplir las características del patron `forward iterator`.

**Casos de uso**
```cpp
    linked_list_t<int> ll;
    // cantidad
    int nhilos = {};
    cin >> nhilos;
    // Hilos
    vector <thread> vhilos(nhilos);
    for (int i = 0; i < nhilos - nhilos/4; ++i)
        vhilos[i] = thread([&ll, i] { ll.push_front(i); });
    for (int i = nhilos - nhilos/4; i < nhilos; ++i)
        vhilos[i] = thread([&ll] { ll.pop_front(); });
    for (auto& hilo: vhilos) hilo.join();
    // Resultado
    cout << ll.size() << endl;
```

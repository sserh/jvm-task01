Дан код.

```java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```
Согласно заданию - требуется прокомментировать строки этого кода в контексте работы JVM.

**Префикс-текст:**  
При выполнении кода начиная с точки входа - все встречающиеся классы передаются в подсистему ClassLoader'ов - `ClassLoaders`.  
Вот эти классы для исследуемого кода:  
1. JvmComprehension
2. Object
3. Integer
4. System
5. String

Данные об этих классах (их имена, методы, поля и прочее) загружаются в область памяти `Metaspace`. 

**Строка 1:**
```java
int i = 1;
```  
В `Stack Memory` во фрейме `main()` переменная i инициализируется значением 1.

**Строка 2:**
```java
Object o = new Object(); 
```  
В `heap` инстанцируется класс `Object`, и в `Stack Memory` во фрейме `main()` создаётся ссылка `o` на экземпляр.

**Строка 3:**
```java
Integer ii = 2;
``` 
В `heap` инстанцируется класс `Integer`, и в `Stack Memory` во фрейме `main()` создаётся ссылка `ii` на экземпляр.

**Строка 4:**
```java
printAll(o, i, ii);
``` 
В `Stack Memory` создаётся фрейм `printAll()`, во фрейме создаются переменные `o`, `i` и `ii`, в которые копируются ссылки на уже созданные в `heap` объекты (для `o` и `ii`)
и значение 1 для переменной примитивного типа int (`i`).

**Строка 5:**
```java
Integer uselessVar = 700;
``` 
В `heap` инстанцируется класс `Integer`, и в `Stack Memory` во фрейме `printAll()` создаётся ссылка `uselessVar` на экземпляр.

**Строка 6:**
```java
System.out.println(o.toString() + i + ii);
``` 
В `Stack Memory` создаются фреймы `toString()`, `println()`. В последнем создаются копии переменных `o`, `i` и `ii`.

**Строка 7:**
```java
System.out.println("finished");
``` 

В `Stack Memory` создаётся фрейм `println()`. В `heap` создаётся строка `finished`, которая передаётся во фрейм `println()`.
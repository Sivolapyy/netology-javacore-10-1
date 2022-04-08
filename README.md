# Задача "Понимание JVM"

## Код для исследования
```java

public class JvmComprehension { // 1) Класс JvmComprehension будет отдан в систему загрузчиков классов для загрузки.

    public static void main(String[] args) {
        int i = 1;                      // 2)
        Object o = new Object();        // 3)
        Integer ii = 2;                 // 4
        printAll(o, i, ii);             // 5
        System.out.println("finished"); // 6
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 7
        System.out.println(o.toString() + i + ii);  // 8
    }
}

```

## Описание

# Решение задачи "Понимание JVM"

## Описываемый код
```java

public class JvmComprehension { // 1

    public static void main(String[] args) { // 2
        int i = 1;                      // 3
        Object o = new Object();        // 4
        Integer ii = 2;                 // 5
        printAll(o, i, ii);             // 6
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 8
        System.out.println(o.toString() + i + ii);  // 9
    }
}

```

### Описание кода по шагам
1. Класс JvmComprehension будет отдан в систему загрузчиков классов для загрузки (загрузчику ApplicationClassLoader). Данные класса (имя, методы и поля) будут загружены в Metaspace.
2. В момент вызова метода main будет создан фрейм (далее mainFrame) в стеке (Stack Memory). Внутри этого фрейма будут храниться все примитивы (значимые типы) которые есть в методе main.
3. Переменная i значимая, поэтому она будет создана внутри фрейма mainFrame в стеке (Stack Memory).
4. В куче (heap) будет создан объект Object, далее в mainFrame будет создана переменная о, а её значением будет ссылка на созданный в куче объект Object.
5. По аналогии с шагом 4 будет создан объект 2 в куче, а в mainFrame будет создана переменная ii в которой будет ссылка на объект 2.
6. В момент вызова метода будет создан новый фрейм в стеке, в этом фрейме будут созданы новые переменные o, i и ii, их значением будут ссылки на соответствующие переменные из mainFrame.
    + 6.1 (8) Аналонично шагу 5.
    + 6.2 (9) Аналогично шагу 8, за исключением того, что переданы будут три новые переменные, значением которых будут ссылки на о, i, ii.
7. Класс System будет загружен BootStrap ClassLoader'ом (если я все правильно понял :) ). Будет создан новый фрейм в стеке (Stack Memory), и в него будет передана новая строка "finished".
8. Сборщик мусора собирает объекты только из кучи, он делает это путём принципа достижимости, т.е. строится граф достижимости каждого объекта, после этого все НЕдостижимые (неиспользуемые) объекты удаляются. Из стека все значимые типы (переменные) удаляются автоматически сразу после выполнения.

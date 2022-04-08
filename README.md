# Решение задачи "Понимание JVM"

## Описываемый код
```java

public class JvmComprehension { // 1) Класс JvmComprehension будет отдан в систему загрузчиков классов для загрузки (загрузчику ApplicationClassLoader).
                                //    Данные класса (имя, методы и поля) будут загружены в Metaspace.

    public static void main(String[] args) { // 2) В момент вызова метода main будет создан фрейм (далее mainFrame) в стеке (Stack Memory). Внутри этого фрейма буду                                                  //      храниться все примитивы (значимые типы) которые есть в методе main.
        int i = 1;                      // 3) Переменная i значимая, поэтому она будет создана внутри фрейма mainFrame
        Object o = new Object();        // 4) В куче (heap) будет создан объект, далее в mainFrame будет создана переменная о, а её значением будет ссылка на созданный в                                         //    куче объект
        Integer ii = 2;                 // 5) По аналогии с шагом 2 будет создан объект 2 в куче, а в mainFrame будет создана переменная ii в которой будет ссылка на                                             //    объект 2.
        printAll(o, i, ii);             // 6) В момент вызова метода будет создан новый фрейм в стеке, в этом фрейме будут созданы новые переменные o, i и ii, их                                                 //    значением будут ссылки на соответствующие переменные из mainFrame
        System.out.println("finished"); // 7) Класс System будет загружен BootStrap ClassLoader'ом (если я все правильно понял :) ). 35:11 - в видео с лекции
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 8
        System.out.println(o.toString() + i + ii);  // 9
    }
}

```

## Описание кода по шагам

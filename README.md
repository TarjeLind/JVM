Код для исследования

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

Общее описание алгоритма программы

   ##**1-Application ClassLoader загружает класс JvmComprehension.**
      В Metaspace помещается мета-информация о классе JvmComprehension: имя, методы, поля.
      В Stack Memory помещается фрейм метода main.
      Переменная i также попадает в Stack Memory (фрейм main).
      
   **2-Bootstrap ClassLoader/Platform ClassLoader загружают класс Object.**
      В Metaspace помещается мета-информация о классе Object: имя, методы, поля.
      В heap попадает обект Object.
      В Stack Memory (фрейм метода main) помещается ссылка на объект Object.
      
   **3-Bootstrap ClassLoader/Platform ClassLoader загружают класс Integer**
      В Metaspace помещается мета-информация о классе Integer: имя, методы, поля.
      В heap попадает объект Integer.
      В Stack Memory (фрейм метода main) помещается ссылка на объект Integer.
      
   **4-В Stack Memory помещается фрейм метода printAll.**
      Метод обращается к heap для получения 1го параметра - объекта Object.
      Метод обращается к Stack Memory для получения 2го аргумента - int.
      Метод обращается к heap для получения 3го аргумента - объекта Integer.
      
   **5-Загрузка класса не происходит, поскольку уже загружен ранее.**
      В heap попадает новый объект Integer.
      В фрейм метода printAll (Stack Memory) помещается ссылка на объект Integer.
      
   **6-Bootstrap ClassLoader/Platform ClassLoader загружают класс System.**
      В Metaspace помещаются данные о классе System.
      В Stack Memory создаются фреймы методов out и println.
      Метод println обращается к heap к объекту Object, чтобы вызвать его метод toString.
      
   **7-В Stack Memory создаются фреймы методов out и println.**
      Автоматически создается обект String (аргумент), который помещается в heap.
      В фрейм помещается ссылка на String.
      
   **8-Сборщик мусора выполняет удаление или группировку подходящих или не подходящих объектов.**

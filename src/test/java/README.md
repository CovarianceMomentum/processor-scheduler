# Немного о тестах
Сначала об организации самих тестов: есть интерфейс 
`IntegerRunnerCreator`, при помощи которого создаются
параметризованные тесты на основе **JUnit4**. Таким образом, 
при добавлении новой реализации интерфейса `Runner<T>` или 
при желании сменить тестируемую реализацию достаточно всего 
лишь поменять список тестируемых реализаций в интерфейсе
`IntegerRunnerCreator`.

Сами тесты разделены на несколько смысловых групп:

## RunnerTest

Проверки корректности исполнения в случае, если всё идёт по плану,
то есть не бросается исключений и нет результатов `null`.

### RunnerSimpleTest
Все процессоры возвращают нули, у них нет инпутов.

### RunnerHardTest
Все процессоры возвращают нули, но их граф зависимостей не пуст
и представляет собой *бамбук*.

### RunnerTreeTest
Процессоры возращают сумму своих инпутов и своего индекса, а
граф зависимостей представляет собой дерево, сгенерированное
при помощи *чисел Прюфера*, вот [источник](https://www.geeksforgeeks.org/random-tree-generator-using-prufer-sequence-with-examples/) 
этого генератора.

## ExceptionsTest

Проверки бросания исключений в разных случаях:
 * некорректный граф зависимостей;
 * процессор бросает исключение в рантайме.
 
## CuttingTest

Проверки того, что листы результатов, соответствующих
процессорам, обрезаются если один из них возвращает `null`. 
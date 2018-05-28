# Руководство кодеров-самураев

«Чтобы стать экспертом в практической или научной области, нужны огромный труд и долгое время. Если человек добросовестно трудится каждый час рабочего дня, когда-нибудь он проснется одним из самых компетенткых специалистов своего поколения.» 
Ульям Джеймс.

# Паттерны проектирования
  * Порождающие шаблоны проектирования
    * Abstract Factory — Абстрактная фабрика
    * Builder — Строитель
    * Factory Method — Фабричный метод
    * Prototype — Прототип
    * Singleton — Одиночка
 * Структурные шаблоны проектирования
    * Adapter — Адаптер
    * Bridge — Мост
    * Composite — Компоновщик
    * Decorator — Декоратор
    * Facade — Фасад
    * Flyweight — Приспособленец
    * Proxy — Заместитель
    * Delegation - Делегирование
* Поведенческие шаблоны проектирования
    * Chain of responsibility — Цепочка обязанностей
    * Command — Команда
    * Interpreter — Интерпретатор
    * Iterator — Итератор
    * Mediator — Посредник
    * Memento — Хранитель
    * Observer — Наблюдатель
    * State — Состояние
    * Strategy — Стратегия
    * Template method — Шаблонный метод
    * Visitor — Посетитель
    
* Конечный автомат

# Инструменты языков программирования 
* Выравнивание 
* Битовые поля
* Mixin
* Компоратор 
* Лямбда функции 
* Перечисления 
* Кортежи
* Имянованные параметры

* fold expression
* Parameter pack
* Class template argument deduction
* Constraints and concepts
* Structured binding declaration

# Техники
* Каламбур типизации
* Карирование 
* Частичное применение 
* Сериализация

# Namespace's, type's and template's aliase 
http://en.cppreference.com/w/cpp/language/namespace_alias
http://ru.cppreference.com/w/cpp/language/type_alias

$ TODO

# Модульность кода 
http://en.cppreference.com/w/cpp/language/namespace
* Entity Component System (агрегация) 


https://en.wikibooks.org/wiki/More_C%2B%2B_Idioms

# Probabilistic algorithms and data structures 
* Bloom filter
* Count–min sketch
* HyperLogLog
* Kinetic hanger
* Kinetic heater
* Locality-sensitive hashing
* MinHash
* Quotient filter
* Random binary tree
* Random tree
* Rapidly-exploring random tree
* SimHash
* Skip list
* Treap
* Filtered-Space Saving Top-K
* T-Digest
* Cuckoo Filter

# Event based paradigm  
CPP
* SObjectizer https://habr.com/post/354508/
* C++ Actor Framework 

# Буст в глубину

https://natsys-lab.blogspot.ru/2015/09/fast-memory-pool-allocators-boost-nginx.html

# Генетические алгоритмы 

# Статистические алгоритмы ?
* Алгоритмы голосования

# Многопоточность 
http://www.modernescpp.com/index.php/multithreading-in-c-17-and-c-20

# Программирование для GPU
# Низкоуровневые возможности, апаратно специфичные средства
* ABI
* Calling convention
* [SIMD Extensions](https://laurent-leturgez.com/2015/04/22/simd-extensions-in-and-out-oracle-12-1-0-2/)
* BLOB
* Написание драйверов

 <details>
   <summary> Intrinsic </summary>
   <p>https://software.intel.com/sites/landingpage/IntrinsicsGuide/
    В С/С++ любая сущность, объявленная, но не определённая в пределах компилируемого файла считается внешней. Это относится и к функциям в не меньшей степени, к чем к переменным. Ссылки на внешние функции остаются в скомпилированном объектном файле и будут заменены на обращения к настоящим сущностям только на этапе линковки, если все межмодульные зависимости будут удовлетворены. Не существует никакой разницы между PrivetVasya() и printf() — с точки зрения компилятора обе абсолютно равнозначны и про обе можно сказать «да это просто какие-то внешние функции». Когда идиотские учебники или учителя-недоучки начинают говорить «встроенная функция языка printf()» (а это очень популярный бред) — надо понимать, что это просто глупость, что в язык ничего такого не встроено, что компилятор обрабатывает вызов к printf() на тех же условиях, что и вызов к любой другой функции, да хоть в соседнем файле реализованной. Что касается той же printf() — то это не встроенная функция языка, а функция стандартной библиотеки языка. Стандарт на язык эту функцию описывает, провозглашает её наличие в стандартной библиотеке, но сам компилятор к стандартной библиотеке отношения не имеет — она может появиться на этапе линковки, а может и вообще не появляться.

Тем не менее, есть поистине встроенные функции, для которых в компиляторе на самом деле реализована особая обработка — они называются intrinsic-ами. У разных компиляторов набор intrinsic-ов разный. Intrinsic-ом может быть и функция, которая штатно должна жить в стандартной библиотеке. При вызове intrinsic-функции компилятор генерирует особый код, характерный именно для данной функции: не генерируется никакого call-а, не будет никакого реального вызова и возврата, а будет несколько инструкций, выполняющих нужную задачу. Например очень распространённый intrinsic memcpy() компилируется не в вызов какой-то функции, а в инструкцию repnz movs (пример для x86).

Понятное дело, что в стандартной библиотеке С (libc) для AVR есть некоторые функции, которые обеспечивают задержку. Естественно, это полновесные функции, которые внутри крутят цикл. Если нужна задержка в 1—2 такта, то естественно, такие тяжеловесные функции не подходят. Сделать задержку в 1 такт полноценной (и обыкновенной) функцией нельзя: даже если это будет совершенно пустая функция, инструкция call выполняется за 4 такта, и инструкция ret — ещё 4 такта, итого 8 тактов на вызов пустой функции.

Без малейшей лишней мысли понятно, что задержки в единицы тактов (меньше 8) могут быть реализованы только intrinsic-ами. И теперь, скрестив пальцы, спросим: а есть ли в avr-gcc delay-функции (функции задержки), выполненные как intrinsic-и? Действительно есть такой intrinsic — функция называется __builtin_avr_delay_cycles().

Источник: Фейл gcc (или назвался intrinsic'ом — полезай в оптимизатор)</p>
  </details>
  * Assembler 
  * Микрокод
  # Обеспечение безопасности для embeded устройств  
  https://gcc.gnu.org/onlinedocs/gcc/Integer-Overflow-Builtins.html
  * MISRO C 
  * unit тесты для C 
  1) Выделение всей памяти на стэке или выделение памяти только во время старта программы 





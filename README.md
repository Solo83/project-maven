# project-maven
project-maven-template


Нужно сдНужно сделать исполняемый JAR-файл с игрой на JavaFX через графический движок от JavaRush.
Для этого нужно:

Сделать fork из репозитория https://github.com/vasylmalik/project-maven.git
Скачать свою версию проекта к себе на компьютер. Дальше будем работать с файлом pom.xml.
Добавить зависимости:
org.apache.commons: commons-lang3: 3.12.0
org.openjfx: javafx-controls: 18.0.1
com.javarush: desktop-game-engine:1.0 (об этой зависимости будет отдельное задание)
org.junit.jupiter: junit-jupiter-engine: 5.8.2 (с scope test)
org.mockito: mockito-core: 4.5.1 (с scope test)
Добавить плагины для:
установки зависимости com.javarush: desktop-game-engine:1.0 из библиотеки lib в локальный репозиторий (google в помощь);
плагин maven-compiler-plugin оставить без изменений;
плагин, который соберет все зависимости (с scope compile) и сложит в какую-то директорию при сборке;
плагин maven-jar-plugin, который сделает jar файл, содержащий код игры и зависимости. В этом плагине нужно сконфигурировать файл MANIFEST.MF, чтоб он содержал секции: Class-Path, Main-Class и Rsrc-Main-Class
В Class-Path должны быть прописаны все наши JAR-зависимости.
В Main-Class должен быть прописан класс org.eclipse.jdt.internal.jarinjarloader.JarRsrcLoader, который умеет использовать classpath из JAR-файлов, а также умеет стартовать приложение на JavaFX.
В Rsrc-Main-Class должен быть прописан стартовый класс игры (com.javarush.games.racer.RacerGame).
В плагине maven-surefire-plugin сделать конфигурацию, чтоб тест StrangeTest не запускался при сборке. Остальные тесты должны выполняться.
Добавить секцию “resources”, в которой сказать, что собранные JAR-зависимости это ресурс, чтоб плагин maven-jar-plugin сложил их внутрь JAR-файла в папку lib/
Залить изменения в свой GitHub-репозиторий, отправить ссылку на него преподавателю.

Полезное:

Билд нужно выполнять командой mvn clean install.
апуск игры (через Maven) с целью посмотреть можно выполнить командой mvn javafx:run.
Некоторым плагинам нужно переопределить phase.
В проекте используется версия JDK 18.0.1. Она должна быть скачана у тебя на компе.
При билде через Maven сперва будут ошибки. Читай их внимательно и ты упростишь себе жизнь.
В пакете org.eclipse.jdt.internal.jarinjarloader ничего не изменяй. В нем кастомный класс-лоадер (честно скопированный с StackOverflow), в котором изменен запуск метода main на запуск JavaFX приложения. Использовать только в учебных целях.
Если выполнить все пункты, в результате сборки ты получишь fat-JAR-файл. Запустить и проверить, что все сделано правильно можно командой:
<путь к java 18> -jar <имя результирующего jar файла>

//Пример
"C:\Users\leo12\.jdks\openjdk-18.0.1.1\bin\java.exe" -jar "E:\temp\project-maven-1.0.jar"
В результате ты увидишь:
Билд зависит от твоей операционной системы. То есть, если JAR-файл собран на Windows, его можно выполнить на любом компе с Windows и Java18. И нельзя выполнить на Mac и Linux.

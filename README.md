# Caveman2Project



<h2>Установка и развертывание веб фреймворка Caveman2 на Common Lisp для создания веб приложений</h2>


Ккак запускать фреймворк на коммон лисп для того чтобы создавать веб сайты с использованием функционального языка программирования

<h3>Установка </h3>


Установка достаточно сложная для остальных языков программирования. Все дело именно в сложности работы с виртуальными проектами и программным кодом. Также нет встроенного текстового редактора, к которому так привыклю многие программисты на более современных языках программирования 



1. Установка переменной среды Roswell

Roswell — это установщик/менеджер реализации Lisp, программа запуска и многое другое!

Roswell начинался как инструмент командной строки с целью сделать установку и управление реализациями Common Lisp действительно простыми и легкими.

Roswell теперь превратился в полнофункциональную среду для разработки на Common Lisp и имеет множество функций, которые упрощают тестирование, совместное использование и распространение ваших приложений Lisp. С Roswell мы стремимся вывести сообщество Common Lisp на совершенно новый уровень продуктивности.

Розуэлл все еще находится в стадии бета-тестирования. Несмотря на это, базовые интерфейсы стабильны и вряд ли изменятся. Roswell в настоящее время хорошо работает на Unix-подобных платформах, таких как Linux, macOS и FreeBSD. Roswell также работает с другими операционными системами, но в настоящее время некоторые части или функции могут отсутствовать или работать нестабильно.

[Список проблем](https://github.com/roswell/roswell/issues) с оформлением заказа , если вас интересует, чего не хватает.

См. нашу [вики на github](https://github.com/roswell/roswell/wiki) . Мы предоставляем готовые двоичные файлы для Homebrew для macOS, различных дистрибутивов Linux, а также для Windows .



* <span style="text-decoration:underline;">Linux</span>
* [FreeBSD](https://github.com/roswell/roswell/wiki/Installation#freebsd)
* [macOS (через Homebrew)](https://github.com/roswell/roswell/wiki/Installation#mac-os-x--homebrew)
* <span style="text-decoration:underline;">Windows</span>
* [Сборка из исходного кода](https://github.com/roswell/roswell/wiki/Installation#building-from-source)
1. Для Windows установка передельно простая

Установка scoop в PowerShell с вызовом от имени администратора:

> Set-ExecutionPolicy RemoteSigned -Scope CurrentUser # Optional: Needed to run a remote script the first time

> irm get.scoop.sh | iex



2. Установка roswell через scoop

$ scoop install roswell



3. Установка остальных библиотек

$ ros install               # displays a list of all installable implementations

$ ros install sbcl-bin      # default sbcl

$ ros install sbcl          # The newest released version of sbcl

$ ros install ccl-bin       # default prebuilt binary of ccl

$ ros install sbcl/1.2.0    # A specific version of sbcl

$ ros list installed sbcl   # Listing the installed implementations

$ ros run -- --version      # check which implementation is used

SBCL 1.2.15

$ ros use sbcl/1.2.3        # change the default implementation

Советую именно их скачать и запустить. Roswell непосредственно работает на основе sbcl, который и является одним из библиотек для переменной среды Common Lisp



4. Запуск roswell

запустите ros командой ros run

Далее будем устанавлинвать нужны нам библиотеки для веб фреймворка и будем запускать непосредственно сам сервер

<h3>Скачивание Caveman2</h3>


Скачивание Caveman2 делается через quicklisp. Который их коробки идет в sbcl. Если не так, то можно установить через sbcl или установить по этой документации

[https://www.quicklisp.org/beta/](https://www.quicklisp.org/beta/)

<h4>Установка</h4>


<h4>Caveman2 теперь доступен на [Quicklisp](https://www.quicklisp.org/beta/) .</h4>


<h4>(ql:quickload :caveman2)</h4>


<h3>[Создание скелета проекта](https://github.com/fukamachi/caveman#generating-a-project-skeleton)</h3>


<h4>(caveman2:make-project #P"/path/to/myapp/"</h4>


<h4>                       :author "<Your full name>")</h4>


<h4>;-> writing /path/to/myapp/.gitignore</h4>


<h4>;   writing /path/to/myapp/README.markdown</h4>


<h4>;   writing /path/to/myapp/app.lisp</h4>


<h4>;   writing /path/to/myapp/db/schema.sql</h4>


<h4>;   writing /path/to/myapp/shlyfile.lisp</h4>


<h4>;   writing /path/to/myapp/myapp-test.asd</h4>


<h4>;   writing /path/to/myapp/myapp.asd</h4>


<h4>;   writing /path/to/myapp/src/config.lisp</h4>


<h4>;   writing /path/to/myapp/src/db.lisp</h4>


<h4>;   writing /path/to/myapp/src/main.lisp</h4>


<h4>;   writing /path/to/myapp/src/view.lisp</h4>


<h4>;   writing /path/to/myapp/src/web.lisp</h4>


<h4>;   writing /path/to/myapp/static/css/main.css</h4>


<h4>;   writing /path/to/myapp/t/myapp.lisp</h4>


<h4>;   writing /path/to/myapp/templates/_errors/404.html</h4>


<h4>;   writing /path/to/myapp/templates/index.tmpl</h4>


<h4>;   writing /path/to/myapp/templates/layout/default.tmpl</h4>


<h3>Запуск сервера</h3>


<h4>Это пример, в котором предполагается, что имя вашего приложения — «myapp». Прежде чем запустить сервер, вы должны сначала загрузить свое приложение.</h4>


<h4>(ql:quickload :myapp)</h4>


<h4>В вашем приложении есть названные функции startи stopдля запуска/остановки вашего веб-приложения.</h4>


<h4>(myapp:start :port 8080)</h4>


Краткая документация по маршрутизации:

<h3>Маршрутизация</h3>


Caveman2 предоставляет два способа определения маршрута — @routeи defroute. Вы можете использовать любой из них.

@route— это макрос аннотации, определенный с помощью [cl-annot](https://github.com/arielnetworks/cl-annot) . Требуется метод, URL-строка и функция.

@route GET "/"

(defun index ()

  ...)

;; A route with no name.

@route GET "/welcome"

(lambda (&key (|name| "Guest"))

  (format nil "Welcome, ~A" |name|))

Это похоже на Caveman1, @urlза исключением списка аргументов. Вам не нужно указывать аргумент, если он не требуется.

defrouteэто просто макрос. Он обеспечивает ту же функциональность, что и @route.

(defroute index "/" ()

  ...)

;; A route with no name.

(defroute "/welcome" (&key (|name| "Guest"))

  (format nil "Welcome, ~A" |name|))

Поскольку Caveman основан на ingle, Caveman также имеет систему маршрутизации, подобную [Sinatra](http://www.sinatrarb.com/) .

;; GET request (default)

@route GET "/" (lambda () ...)

(defroute ("/" :method :GET) () ...)

;; POST request

@route POST "/" (lambda () ...)

(defroute ("/" :method :POST) () ...)

;; PUT request

@route PUT "/" (lambda () ...)

(defroute ("/" :method :PUT) () ...)

;; DELETE request

@route DELETE "/" (lambda () ...)

(defroute ("/" :method :DELETE) () ...)

;; OPTIONS request

@route OPTIONS "/" (lambda () ...)

(defroute ("/" :method :OPTIONS) () ...)

;; For all methods

@route ANY "/" (lambda () ...)

(defroute ("/" :method :ANY) () ...)

Шаблоны маршрутов могут содержать «ключевые слова» для помещения значения в аргумент.

(defroute "/hello/:name" (&key name)

  (format nil "Hello, ~A" name))

Вышеуказанный контроллер будет вызываться при доступе к «/hello/Eitaro» или «/hello/Tomohiro» и nameбудет называться «Eitaro» или «Tomohiro», в зависимости от ситуации.

(&key name)почти то же самое, что и лямбда-список Common Lisp, за исключением того, что он всегда допускает использование других ключей.

(defroute "/hello/:name" (&rest params &key name)

  ;; ...

  )

Шаблоны маршрутов также могут содержать параметры «подстановки». Они доступны с помощью splat.

(defroute "/say/*/to/*" (&key splat)

  ; matches /say/hello/to/world

  (format nil "~A" splat))

;=> (hello world)

(defroute "/download/*.*" (&key splat)

  ; matches /download/path/to/file.xml

  (format nil "~A" splat)) 

;=> (path/to/file xml)

Если вы хотите использовать регулярное выражение в правиле URL-адреса, это :regexp tдолжно сработать.

(defroute ("/hello/([\\w]+)" :regexp t) (&key captures)

  (format nil "Hello, ~A!" (first captures)))

Обычно маршруты проверяются на соответствие в том порядке, в котором они определены, и вызывается только первый найденный маршрут, а последующие маршруты игнорируются. Однако маршрут может продолжить проверку совпадений в списке, включив next-route.

(defroute "/guess/:who" (&key who)

  (if (string= who "Eitaro")

      "You got me!"

      (next-route)))

(defroute "/guess/*" ()

  "You missed!")

Вы можете вернуть следующие форматы в результате defroute.



* Нить
* Путь
* Список ответов Clack (содержащий статус, заголовки и тело)

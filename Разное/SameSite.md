SameSite — это механизм защиты браузера, определяющий, когда файлы cookie сайта включаются в запросы, поступающие с других сайтов. Ограничения на использование файлов cookie SameSite обеспечивают частичную защиту от различных межсайтовых атак, включая CSRF, межсайтовые утечки и некоторые CORS-эксплойты.

До появления механизма SameSite браузеры отправляли файлы cookie в каждом запросе к выдавшему их домену, даже если запрос был вызван не связанным с ним сторонним сайтом. SameSite позволяет браузерам и владельцам сайтов ограничить, какие межсайтовые запросы, если таковые имеются, должны включать определённые файлы cookie. 

Начиная с 2021 года Chrome по умолчанию применяет ограничения `Lax` SameSite, если сайт, на котором размещён файл cookie, не задал явно свой собственный уровень ограничений.

### Как работает ограничение 

В контексте ограничений на использование cookie-файлов SameSite под сайтом понимается домен верхнего уровня (TLD), обычно такой, как `.com` или `.net`, плюс один дополнительный уровень доменного имени. Это часто называют TLD+1.

![[Pasted image 20250120101428.png]]

### Уровни ограничения SameSite

![[Pasted image 20250120102532.png]]

https://learn.microsoft.com/ru-ru/microsoftteams/platform/resources/samesite-cookie-update#types-of-cookies

https://www.dev-notes.ru/articles/security/csrf-bypassing-samesite-restrictions/#lax

https://www.dev-notes.ru/articles/security/csrf/

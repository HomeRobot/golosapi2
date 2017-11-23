# golosapi2
New API for GOLOS blockchain based on SQL Database

# Работа с API

1. Обращаться к API можно по адресу http://185.203.243.142/api/ или https://golosapi.today/api/
2. Каждый запрос содержит ряд GET параметров. Обязательный параметр только один, это **method**
3. Результат возвращается в виде массива в формате json
4. Пример запроса:
    `http://185.203.243.142/api/?method=getdiscussions&count=20&author=captain&tags=ru--golos&ignore_body`
5. Можно вернуть в том числе и сам текст SQL запроса, указав параметр **sql**

# Описание методов
## getdiscussions
Метод возвращает посты верхнего уровня. Все параметры не обязательные. По умолчанию возвращается 100 последних записей.
Параметры метода:
- **count** - количество возвращаемых записей, не более 100. 
- **offset** - количество пропускаемых записей
- **order** - порядок сортировки. Может принимать значения id, tx_id, author, title, timestamp с модификатором *desc* в том числе.
- **author** - ник автора постов
- **title** - заголовок поста полностью или его часть
- **search** - поисковая фраза, по которой будет произведен поиск в заголовке и теле поста. В выдачу попадут только те посты в которых найдена указанная фраза. Не забывайте экранировать этот параметр
- **from** - дата в формате YYYY-MM-DD H:i:s начиная с которой будут выводиться посты
- **to** - дата в формате YYYY-MM-DD H:i:s по которую будут выводиться посты
- **category** - набор тэгов через запятую, которые являются основной категорией поста. Будут выбраны только те посты, в которых указана данная категория
- **exclude_category** - набор тэгов через запятую, которые являются основной категорией поста. Будут выбраны только те посты, в которых **не** указана данная категория
- **tags** - набор тэгов через запятую. Будут выбраны только те посты, в которых есть хотя бы один из этих тэгов. 
- **exclude_tags** - набор тэгов через запятую. Будут **исключены** те посты, в которых есть хотя бы один из этих тэгов. Имеет приоритет над набором *tags*
- **ignore_body** - не добавляет в результаты выдачи тело поста

## getpost
Метод возвращает информацию о посте. 
Параметры метода: 
- **permlink** - идентификатор записи
- **author** - ник автора поста
- **ignore_body** - не добавляет в результаты выдачи тело поста

## getvotes
Метод возвращает информацию о голосах, отданных за пост.
Параметры метода: 
- **permlink** - идентификатор записи
- **author** - ник автора поста

## getvoted
Метод возвращает информацию о том было ли голосование за пост указанного автора.
- **permlink** - идентификатор записи
- **author** - ник автора поста
- **voter** - ник голосующего

## getcomments
Метод возвращает информацию о комментариях к посту. Комментарии возвращаются все, упорядоченные иерархически при помощи полей parent_permlink и depth.
Параметры метода: 
- **permlink** - идентификатор записи
- **author** - ник автора поста

## getnewbies
Метод возвращает последние посты от новичков - авторов с 1 или 2 постами.
Параметры метода: 
- аналогичны параметрам метода **getdiscussions**

## getfollowers
Метод возвращает подписчиков указанного автора
Параметры метода: 
- **login** - ник автора 

## getfollowing
Метод возвращает на кого подписан указанный автор
Параметры метода: 
- **login** - ник автора 

## gettransfers
Метод возвращает информацию по переводам между пользователями
Параметры метода:
- **from** - логин отправителя
- **to** - логин получателя
- **count** - количество строк (не более 100)
- **offset** - смещение от начала выборки
- **order** - порядок сортировки
- **from_date** - начиная с указанной даты
- **to_date** - по указанную дату

# KeyAuth-Python-Пример
Пример KeyAuth на Python для https://keyauth.ru система аутентификации.

## **Ошибки**

Если пример по умолчанию, не добавленный в ваше программное обеспечение, работает неправильно, пожалуйста, присоединяйтесь к серверу Discord https://discord.gg/keyauth и отправьте сообщение о проблеме в канале `#ошибки`.

Однако мы **НЕ** предоставляем поддержку для добавления KeyAuth в ваш проект. Если вы не можете в этом разобраться, вам следует воспользоваться Google или YouTube, чтобы узнать больше о языке программирования, на котором вы хотите продавать программу.

## Лицензия на авторское право

KeyAuth лицензирован по **эластичной лицензии 2.0**

* Вы не имеете права предоставлять программное обеспечение третьим лицам в качестве размещенного или управляемого
сервиса, если сервис предоставляет пользователям доступ к какому-либо существенному набору
функций программного обеспечения.

* Вы не имеете права перемещать, изменять, отключать или обходить функциональные возможности лицензионного ключа
в программном обеспечении, а также вы не имеете права удалять или скрывать какие-либо функциональные
возможности программного обеспечения, защищенные лицензионным ключом.

* Вы не имеете права изменять, удалять или скрывать какие-либо уведомления о лицензировании, авторских правах или другие уведомления
лицензиара в программном обеспечении. Любое использование товарных знаков лицензиара регулируется
применимым законодательством.

Благодарим вас за ваше согласие, мы усердно работаем над разработкой KeyAuth и не одобряем нарушения наших авторских прав.

## **Проблемы с подключением клиента?**

Это распространено среди всех систем аутентификации. Запутывание программ приводит к ложным срабатываниям антивирусных сканеров, и в масштабах KeyAuth это воспринимается как вредоносный домен. Итак, `keyauth.ru " были заблокированы многими интернет-провайдерами. для панели управления, панели реселлера, панели клиента используйте `keyauth.ru `

Для API, `keyauth.ru "не сработает, потому что я намеренно заблокировал его там, так что `keyauth.ru "также не блокируется. Итак, вам следует создать свой собственный домен и следовать этому обучающему видео https://www.youtube.com/watch?v=a2SROFJ0eYc . В обучающем видео показано, как создать доменное имя на 100% бесплатно, если вы не хотите его приобретать.

## **Как скомпилировать?**

Вы можете использовать либо Pyinstaller, либо Nuitka.

Связи:
- Нутика: https://nuitka.net/
- Pyinstaller: https://pyinstaller.org/

Pyinstaller Установщик:
- Базовая команда: `pyinstaller --onefile main.py `

Нутика:
- Базовая команда: `python -m nuitka --follow-imports --onefile main.py `

## **Определение экземпляра `KeyAuthApp`**

Визит https://keyauth.ru/app / и выберите свое приложение, затем перейдите на вкладку **Python**

Это предоставит вам код, который вы должны заменить в `main.py ` файл.

```PY
keyauthapp = api(
    name = "example", #App name (Manage Applications --> Application name)
    ownerid = "JjPMBVlIOd", #Owner ID (Account-Settings --> OwnerID)
    secret = "db40d586f4b189e04e5c18c3c94b7e72221be3f6551995adc05236948d1762bc", #App secret(Manage Applications --> App credentials code)
    version = "1.0",
    hash_to_check = getchecksum()
)
```

## **Инициализировать приложение**

Вам не нужно добавлять какой-либо код для инициализации. Ключ аутентификации будет инициализирован при создании определения экземпляра.

## **Отображение информации о приложении**

```py
keyauthapp.fetchStats()
print(f"""
App data:
Number of users: {keyauthapp.app_data.numUsers}
Number of online users: {keyauthapp.app_data.onlineUsers}
Number of keys: {keyauthapp.app_data.numKeys}
Application Version: {keyauthapp.app_data.app_ver}
Customer panel link: {keyauthapp.app_data.customer_panel}
""")
```

## **Проверьте правильность сеанса**

Используйте это, чтобы узнать, вошел ли пользователь в систему или нет.

```py
print(f"Current Session Validation Status: {keyauthapp.check()}")
```

## **Проверьте статус черного списка**

Проверьте, внесен ли HWID или IP-адрес в черный список. Вы можете добавить это, если хотите, просто чтобы убедиться, что никто не сможет открыть вашу программу менее чем на секунду, если они занесены в черный список. Однако, если вы не возражаете, чтобы пользователь, занесенный в черный список, пользовался программой в течение нескольких секунд, пока он не попытается войти в систему и зарегистрироваться, и вы заботитесь о том, чтобы программа была максимально быстрой для ваших пользователей, тогда вам не следует использовать эту функцию. Если пользователь, внесенный в черный список, попытается войти в систему / зарегистрироваться, сервер проверки подлинности ключей проверит, внесен ли он в черный список, и, если да, отклонит вход. Таким образом, функция проверки черного списка - это просто вспомогательная функция, которая необязательна.

```py
if keyauthapp.checkblacklist():
    print("You've been blacklisted from our application.")
    os._exit(1)
```

## **Войдите в систему с помощью имени пользователя/пароля**

```py
user = input('Provide username: ')
password = input('Provide password: ')
keyauthapp.login(user, password)
```

## **Зарегистрируйтесь с помощью имени пользователя/пароля/ключа**

```py
user = input('Provide username: ')
password = input('Provide password: ')
license = input('Provide License: ')
keyauthapp.register(user, password, license)
```

## ** Обновить имя пользователя/ключ**

Используется для того, чтобы пользователь мог добавить дополнительное время к своей учетной записи, запросив новый ключ.

> **Предупреждение**
> Для обновления учетной записи пароль не требуется. Таким образом, в отличие от функций входа в систему, регистрации и лицензирования - вы не должны **** входить в систему пользователя после успешного обновления.

```py
user = input('Provide username: ')
license = input('Provide License: ')
keyauthapp.upgrade(user, license)
```

## **Войдите в систему, используя только лицензионный ключ**

Пользователи могут использовать эту функцию, если их лицензионный ключ никогда ранее не использовался и если он использовался ранее. Поэтому, если вы планируете просто разрешить пользователям использовать ключи, вы можете удалить функции входа в систему и регистрации из своего кода.

```py
key = input('Enter your license: ')
keyauthapp.license(key)
```

## **Пользовательские данные**

Отображать информацию для текущего пользователя, вошедшего в систему.

```py
print("\nUser data: ")
print("Username: " + keyauthapp.user_data.username)
print("IP address: " + keyauthapp.user_data.ip)
print("Hardware-Id: " + keyauthapp.user_data.hwid)

subs = keyauthapp.user_data.subscriptions  # Get all Subscription names, expiry, and timeleft
for i in range(len(subs)):
    sub = subs[i]["subscription"]  # Subscription from every Sub
    expiry = datetime.utcfromtimestamp(int(subs[i]["expiry"])).strftime(
        '%Y-%m-%d %H:%M:%S')  # Expiry date from every Sub
    timeleft = subs[i]["timeleft"]  # Timeleft from every Sub

    print(f"[{i + 1} / {len(subs)}] | Subscription: {sub} - Expiry: {expiry} - Timeleft: {timeleft}")
print("Created at: " + datetime.utcfromtimestamp(int(keyauthapp.user_data.createdate)).strftime('%Y-%m-%d %H:%M:%S'))
print("Last login at: " + datetime.utcfromtimestamp(int(keyauthapp.user_data.lastlogin)).strftime('%Y-%m-%d %H:%M:%S'))
print("Expires at: " + datetime.utcfromtimestamp(int(keyauthapp.user_data.expires)).strftime('%Y-%m-%d %H:%M:%S'))
print(f"Current Session Validation Status: {keyauthapp.check()}")
```

## **Показать список онлайн-пользователей**

```py
onlineUsers = keyauthapp.fetchOnline()
OU = ""  # KEEP THIS EMPTY FOR NOW, THIS WILL BE USED TO CREATE ONLINE USER STRING.
if onlineUsers is None:
    OU = "No online users"
else:
    for i in range(len(onlineUsers)):
        OU += onlineUsers[i]["credential"] + " "

print("\n" + OU + "\n")
```

## **Переменные приложения**

Строка, которая хранится на стороне сервера Key Auth. На панели мониторинга вы можете выбрать для каждой переменной аутентификацию (доступ могут получить только зарегистрированные пользователи) или не аутентификацию (любой пользователь может получить доступ до входа в систему). Они являются глобальными и статичными для всех пользователей, в отличие от пользовательских переменных, которые будут рассмотрены ниже в этом разделе.

```py
* Get normal variable and print it
data = keyauthapp.var("varName")
print(data)
```

## **Пользовательские переменные**

Пользовательские переменные - это строки, хранящиеся на стороне сервера Key Auth. Они специфичны для пользователей. Их можно установить на панели мониторинга на вкладке "Пользователи", через SellerAPI или через ваш загрузчик, используя приведенный ниже код. "discord" - это имя пользовательской переменной, по которому вы извлекаете пользовательскую переменную. `test#0001` - это данные переменной, которые вы получаете при извлечении пользовательской переменной.

```py
* Set up user variable
keyauthapp.setvar("varName", "varValue")
```

И вот как вы извлекаете пользовательскую переменную:

```py
* Get user variable and print it
data = keyauthapp.getvar("varName")
print(data)
```

## **Журналы приложений**

Может использоваться для регистрации данных. Хорошо подходит для предупреждений об отладке и, возможно, для отладки ошибок. Если вы настроите Discord webhook в настройках приложений панели мониторинга, он будет отправлять сообщения журнала на ваш Discord webhook, а не сохранять их на сайте. Рекомендуется установить Discord webhook, так как логи на сайте удаляются через 1 месяц после отправки.

Вы можете использовать функцию регистрации до входа в систему и после входа в систему.

```py
* Log message to the server and then to your webhook what is set on app settings
keyauthapp.log("Message")
```

## **Забанить пользователя**

Заблокируйте пользователя и внесите в черный список его HWID и IP-адрес. Хорошая функция для вызова, если вы используете защиту от отладки и обнаружили попытку вторжения.

Функция работает только после входа в систему.

```py
keyauthapp.ban()
```

## **Веб-хуки на стороне сервера**

Обучающее видео https://www.youtube.com/watch?v=ENRaNPPYJbc

> **Примечание**
> Прочитайте документацию для веб-подключений KeyAuth здесь https://docs.keyauth.ru/website/dashboard/webhooks

Безопасно отправляйте HTTP-запросы по URL-адресам, не допуская утечки URL-адреса в вашем приложении. Вам обязательно следует использовать, если вы хотите отправлять запросы в SellerAPI из своего приложения, в противном случае, если вы этого не сделаете, вы передадите свой ключ продавца всем. И тогда кто-то может испортить ваше приложение.

1-й пример - это как отправить запрос без данных POST. просто запрос GET на URL-адрес. `7kR0UedlVI` - это идентификатор веб-узла, `https://keyauth.ru/api/seller/?sellerkey=sellerkeyhere&type=black ` - это то, что вы должны указать в качестве конечной точки webhook на панели мониторинга. Это та часть, которую вы не хотите, чтобы пользователи видели. И тогда у вас есть `&ip=1.1.1.1&hwid=abc` в вашем программном коде, который будет добавлен к конечной точке webhook на сервере keyauth, а затем запрос будет отправлен.

2-й пример включает в себя данные post. это данные формы. это пример запроса к KeyAuth API. `7kR0UedlVI` - это идентификатор веб-узла, `https://keyauth.ru/api/1.2 /` - это конечная точка webhook.

3-й пример включал данные post, хотя это JSON. Это пример запроса к Discord webhook `7kR0UedlVI` - это идентификатор webhook, `https://discord.com/api/webhooks /...` - это конечная точка webhook.

```py
* example to send normal request with no POST data
data = keyauthapp.webhook("7kR0UedlVI", "&ip=1.1.1.1&hwid=abc")

* example to send form data
data = keyauthapp.webhook("7kR0UedlVI", "", "type=init&name=test&ownerid=j9Gj0FTemM", "application/x-www-form-urlencoded")

* example to send JSON
data = keyauthapp.webhook("7kR0UedlVI", "", "{\"content\": \"webhook message here\",\"embeds\": null}", "application/json")
```

## **Загрузить файл**

> **Примечание**
> > Ознакомьтесь с документацией по ключевым файлам аутентификации здесь https://keyauth.readme.io/reference/introduction

Обеспечьте безопасность файлов, предоставив KeyAuth ссылку для скачивания вашего файла на панели управления KeyAuth. Убедитесь, что это прямая ссылка для скачивания (как только вы перейдете по ссылке, она начнет загружаться без вашего нажатия на что-либо). Функция загрузки KeyAuth предоставляет байты, а затем вы сами решаете, что с ними делать. В этом примере показано, как записать его в файл с именем `text.txt ` в той же папке, что и программа, хотя вы могли бы выполнить ее с помощью RunPE или чего угодно еще.

`385624` - это идентификатор файла, который вы получаете на панели мониторинга после добавления файла.

```py
* Download Files form the server to your computer using the download function in the api class
bytes = keyauthapp.file("385624")
f = open("example.exe", "wb")
f.write(bytes)
f.close()
```

## **Каналы чата**

Разрешите пользователям общаться между собой в вашей программе.

Пример из примера формы о том, как извлекать сообщения чата.

```py
* Get chat messages
messages = keyauthapp.chatGet("CHANNEL")

Messages = ""
for i in range(len(messages)):
Messages += datetime.utcfromtimestamp(int(messages[i]["timestamp"])).strftime('%Y-%m-%d %H:%M:%S') + " - " + messages[i]["author"] + ": " + messages[i]["message"] + "\n"

print("\n\n" + Messages)
```

Пример того, как отправить сообщение в чате.

```py
* Send chat message
keyauthapp.chatSend("MESSAGE", "CHANNEL")
```

# WSL port forwarding

Как же без мороки открыть порты на wsl? Расскажу здесь. 
Заранее приготовьте: терпение, белый ip, немного времени и комп с wsl.


## План

1. [Зайти в админку маршрутизатора](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%B7%D0%B0%D0%B9%D1%82%D0%B8-%D0%B2-%D0%B0%D0%B4%D0%BC%D0%B8%D0%BD%D0%BA%D1%83-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B0)
2. [Найти ip внутри сети](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%BD%D0%B0%D0%B9%D1%82%D0%B8-ip-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D1%81%D0%B5%D1%82%D0%B8)
3. [Открыть нужные порты на маршрутизаторе](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8C-%D0%BD%D1%83%D0%B6%D0%BD%D1%8B%D0%B5-%D0%BF%D0%BE%D1%80%D1%82%D1%8B-%D0%BD%D0%B0-%D0%BC%D0%B0%D1%80%D1%88%D1%80%D1%83%D1%82%D0%B8%D0%B7%D0%B0%D1%82%D0%BE%D1%80%D0%B5)
4. [Добавить правила в брандмауэр](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D0%B0-%D0%B2-%D0%B1%D1%80%D0%B0%D0%BD%D0%B4%D0%BC%D0%B0%D1%83%D1%8D%D1%80)
5. [Проверка, доступны ли порты не внутри сети](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%BD%D1%8B-%D0%BB%D0%B8-%D0%BF%D0%BE%D1%80%D1%82%D1%8B-%D0%BD%D0%B5-%D0%B2%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D1%81%D0%B5%D1%82%D0%B8)
6. [Пара комманд в powershell](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%BF%D0%B0%D1%80%D0%B0-%D0%BA%D0%BE%D0%BC%D0%BC%D0%B0%D0%BD%D0%B4-%D0%B2-powershell)
7. [Снова проверка](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D1%81%D0%BD%D0%BE%D0%B2%D0%B0-%D0%BF%D1%80%D0%BE%D0%B2%D0%B5%D1%80%D0%BA%D0%B0)
8. [Готово!](https://github.com/Kolya080808/WSL-port-forwarding/tree/main#%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BE)


## Основное содержание

### Зайти в админку маршрутизатора

Обычно ip роутера это 192.168.1.1 или 192.168.0.1, но бывают случаи, когда он не такой, и тогда нужно это проверить. Это можно просто сделать, зайдя в консоль и прописав ipconfig:

![image](https://github.com/user-attachments/assets/738a472e-b843-428f-9d04-ca1539716144)

Ну и просто вбиваем его в хроме или любом другом браузере:

![image](https://github.com/user-attachments/assets/b9f376ce-691f-4bdd-b986-1b4a5d9a2902)


Далее он нас просит войти, мы входим (если вдруг кто не знает, обычно стоит логин и пароль admin и admin, но иногда производители сзади на наклейке и просто по дефолту ставят свои учетные данные, так что посмотрите их для своего производителя).


И вот мы вошли!

![image](https://github.com/user-attachments/assets/ffe5cd33-168c-4612-b7a5-3fe37e26db9f)

### Найти ip внутри сети

Здесь мы опять обращаемся к cmd. **ВАЖНО - взять ip НЕ WSL, А КОМПЬЮТЕРА**:

![image](https://github.com/user-attachments/assets/9c8b4bcd-a78d-4301-aca2-c047ecb41600)

В принципе это все.

### Открыть нужные порты на маршрутизаторе

В данном случае у меня роутер с edgeos, так что здесь все отличается. Поэтому скажу так: вам надо найти Port Forwarding или какую-то подобную настройку на вашем роутере. У меня она находится в Firewall/NAT --> Port Forwarding.


![image](https://github.com/user-attachments/assets/b1c15c6f-cefd-4100-a74a-22524a4d46ea)

Иногда он просит ввести, куда мы подключили WAN провод и какой LAN провод используется. На картинке я его уже указал.
После того, как вы это сделали, необходимо добавить правило. В моем случае вы вводите сначала порт (любой, который вам надо), потом протокол (UDP/TCP), потом тот ip, который мы нашли в прошлом шаге, далее тот же порт, ну и название/описание.

** ВАЖНО! НЕ СТАВЬТЕ ПОРТЫ 22 ИЛИ 80, ТАК КАК ВЫ ВОЗМОЖНО НЕ СМОЖЕТЕ ПОЛУЧИТЬ ДОСТУП К РОУТЕРУ. Я ЕГО ПОСТАВИЛ ПОТОМУ, ЧТО УВЕРЕН, ЧТО ДОСТУП К НЕМУ Я ПОЛУЧУ. **

Добавив правила, нажмите apply. Готово!

### Добавить правила в брандмауэр

Это нужно сделать обязательно, так как иначе компьютер просто не будет принимать подключения по этим портам ни в каком случае, пока вы этого не сделаете.

В строке поиска в windows пишем `Брандмауэр`, открываем то, что начинается со слова "Мониторинг".

![image](https://github.com/user-attachments/assets/8929936a-b3ff-4392-9d1d-92147a8e748e)

![image](https://github.com/user-attachments/assets/a46cb5df-7581-4ee5-a859-9578bda47068)


Далее надо зайти в "Правила для входящих подключений", справа, и нажать "Создать правило", слева.

![image](https://github.com/user-attachments/assets/67da83ab-2c37-4b08-9247-d624bc6796da)

![image](https://github.com/user-attachments/assets/2a7b2358-f0c4-4f1a-b8f8-8eb175256b05)


У нас выплывает вот такое окно. В нем мы указываем "Для порта".

![image](https://github.com/user-attachments/assets/603db5a1-a5b5-44ff-b64e-70b51b06d333)

Нажимаем далее, и выбираем протокол TCP (если вам так же необходим udp, просто добавьте новое правило, перечитав данный пункт, и вместо tcp выберите udp), а в строке снизу впишите порты, которые вы открыли через запятую, и нажмите далее.

![image](https://github.com/user-attachments/assets/3585749d-0d70-4f18-85bc-4e9b39b0ba3e)

Здесь выберите "Разрешить подключения", нажмите далее, выберите все возможные пункты, назовите правило (я его назвал "Для хакинга"), и нажмите готово.

![image](https://github.com/user-attachments/assets/71948db8-be99-4d38-875b-ac2ac4b16957)

![image](https://github.com/user-attachments/assets/e9ea385b-c428-4f5c-b68e-389e37550b55)

![image](https://github.com/user-attachments/assets/e9ccf23d-ea7f-43cc-8457-213eb7242656)

Чтобы проверить, есть ли правило, попробуйте найти его в поле посередине. У меня оно появилось.

![image](https://github.com/user-attachments/assets/d61cf222-8f25-4d9c-a12c-a0b194d45072)

### Проверка, доступны ли порты не внутри сети

Я это делал так же через cmd. Сначала я прописал `curl 2ip.ru`, чтобы узнать свой внешний ip, а потом `python -m http.server 8080` и зашел по внешнему ip и порту через браузер.

![image](https://github.com/user-attachments/assets/16819578-2f00-40dc-8d46-20a5acbfffc7)


![image](https://github.com/user-attachments/assets/a5b6e802-cb09-4d61-8985-17ce0a7be392)

Они доступны! Ура!

*если у вас они не доступны, проверьте, все ли вы сделали правильно в прошлых шагах*

### Пара комманд в powershell


Далее необходимо открыть powershell и ввести определенные команды, чтобы компьютер перенаправлял подключения со своего ip на ip wsl.
Сначала запускаем powershell от имени администратора, введя в поиске `powershell`, нажав правой кнопкой мыши и выбрав `запустить от имени администратора`. У меня это выглядит так:

![image](https://github.com/user-attachments/assets/78c68ed1-1116-4404-afe4-d516526a50af)

У вас, скорее всего, так:

![image](https://github.com/user-attachments/assets/689748da-933a-414c-9b4a-02fcc097c779)

В строке мы вводим вот такую команду:
```powershell
netsh interface portproxy add v4tov4 listenport={port} listenaddress=0.0.0.0 connectport={port} connectaddres=$($(wsl hostname -I).Trim()); 
```
#### Давайте ее разберем:
1. netsh - это служебная программа на базе командной строки, которая позволяет показывать или изменять конфигурацию сети компьютера
2. interface - настройка или показывание настроек определенного интерфейса
3. portproxy - команда для перенаправления определенного порта этого компьютера на другой
4. add - добавление интерфейса
5. v4tov4 - название интерфейса (вы можете использовать любое другое на английском языке)
6. listenport - тот порт, на который компьютер будет ждать подключения
7. {port} - ваш порт
8. listenaddress=0.0.0.0 - мы говорим, что мы ждем подключения только на этот компьютер
9. connectport - тот порт, на который нам нужно направить подключение (советую поставить такой же, как и в listenport)
10. connectaddres=$($(wsl hostname -I).Trim()); - чтобы постоянно не менять адрес перенаправления, мы сделали вот такую команду. Если же у вас стоит несколько дистрибутивов, то можно сделать вместо этой команды вот такую: `connectaddres=$($(wsl -d {distribution} hostname -I).Trim());`, где {distribution} - ваш дистрибутив.

Мы делаем так с каждым портом. Чтобы проверить, добавился ли интерфейс, мы можем ввести команду 
```powershell
netsh interface portproxy show v4tov4
```

![image](https://github.com/user-attachments/assets/b9cb11af-89b1-47e8-b753-16e7532942f7)

У меня все хорошо.

Чтобы удалить правило, мы можем ввести такую команду:
```powershell
netsh interface portproxy delete v4tov4 listenaddress=0.0.0.0 listenport={port}
```

### Снова проверка

Теперь надо проверить, работают ли правила. Все команды теперь надо вводить в wsl. Я проверял это так же, как и в одном из прошлых шагов (`python3 -m http.server 8080`):

![image](https://github.com/user-attachments/assets/c0e73036-917f-4ab8-b012-38768e77fec2)

![image](https://github.com/user-attachments/assets/7bc9fcea-e29e-46e4-b376-d7ff24aaf44d)

### Готово!

Все работает. Если у вас есть какие-то вопросы - открывайте [issue](https://github.com/Kolya080808/WSL-port-forwarding/issues/new), и я на них отвечу.
Написал я это 15.02.2025, проверил на следующий день, вроде ничего не упустил. Но если все-таки да - пишите [туда же](https://github.com/Kolya080808/WSL-port-forwarding/issues/new), просто добавьте в Labels "enchancement".

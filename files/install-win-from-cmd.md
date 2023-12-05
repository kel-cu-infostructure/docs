#### {"title": "Установка Winodws из под командную строку и Windows PE", "ignoreList": true, "hideContact": false}
# Установка Windows из под командную строку и Windows PE
Сегодня я покажу как можно установить Windows через командную строку. Тут причины безграничны, кто-то устанавливает в обход системных требований, кому-то удобнее так и т.д.
Мне лично для обхода ограничений и удобства настроек.

Установку я буду показывать Windows 10 LTSC 2019 с её образом, виртуальная машина VMWare 17

## Загрузка в Windows PE [Pre-installation Environment]
Грузимся в образ, как заходить в биос и бут меню я в душе не чаю. На ASUS может быть F2 [У меня на ноуте] или DEL [На старой мат. плате]<br>
Нажимаем сочитание клавиш `Shift+F10`, и появится командная строка.

### Обновление системы [Если хотите установить как обновление]
`Скоро(tm)`
### Разметка диска
Прописываеи команду `diskpart`.<br>
Теперь нам нужно найти нужный диск, прописываем `list disk`<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/51a79882-2bd7-4ebd-a9be-dfedd700cf82)<br>
В моём случае это чистый диск 0 на 60 гигов<br>
Выбираем диск `select disk %number%`<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/046619ba-3b60-4524-9637-04a9d9730918)<br>
Конвертируем в GPT`(UEFI)`/MBR`(BIOS)`<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/77496623-b3ee-410b-8350-d5e97289d413)<br>
Теперь нам нужно создать разделы<br>
EFI Раздел<br>
```
create partition efi size=500m
assign letter=G:
```
Системный раздел
```
create partition primary
assign letter=C:
``` 
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/4b0dc79c-4dd1-4424-a19d-c9a66ad76db2)<br>
Теперь можно спокойно выйти из программы `exit` и начать форматировать разделы.<br>
Пропишем 2 одинаковые команды.<br>
Форматирование EFI раздела.<br>
```
format G: /fs:fat32 /q 
```
Форматирование системного раздела.<br>
```
format C: /fs:ntfs /q
```
> `G: / C:` - Буквы нужных разделов<br>
> `/fs:(fat32/ntfs)` - Файловая система<br>
> `/q` - Quick format [Быстрое форматирование]<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/05501391-49d0-4646-83f5-493523aece70)<br>

### Установка Windows
Теперь нам нужно через программу Dism применить образ системы. <br>
Нам нужно найти наш install.wim(.esd в новых версиях). Найти можно через блокнот изменив File name(Название файла): install.*<br>
Обычно он находится в диске установщика (Не раздел BOOT!!!) и в папке sources.<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/6fd4f88e-af29-4a74-95e2-8358cb9bc2b6)<br>
Переходим в Dism, если у вас оригинальная сборка и мульти-издания, нам нужно узнать индекс нужного издания.<br>
`dism /Get-WimInfo /wimfile=D:/sources/install.wim(.esd)`<br>
> На скриншоте видно что у меня два издания, я выберу первый. Вы смотрите сами и ставите себе нужный

![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/bac1929d-ce24-45b9-b0a6-637ee6ef17f4)<br>
Теперь копируем файлы системы на системный диск<br>
`dism /Apply-Image /ImageFile:D:\sources\install.wim /index:1 /ApplyDir:C:\`<br>
Waiting :)<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/6559d737-d249-4d11-b6ec-b4d11715d7d2)<br>

Теперь нам нужно настроить загрузчик<br>
`bcdboot C:\Windows /s G: /f (UEFI/BIOS)`<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/da8affbc-2626-45c5-ad0d-860ddcb83a66)<br>
Теперь можно перезагрузиться в систему<br>
`wpeutil reboot`<br>
![image](https://github.com/simply-kel/simplykel.ru/assets/86980879/7205343e-ac47-4b30-b000-38249c27030a)<br>
Добро пожаловать в операционную систему Windows! (Ненавижу Windows, честно)


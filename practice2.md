# Практические задания 2: Беспроводные сети

В качестве "скелета" для приложения под RIOT, работающего с LoRaWAN, можно использовать пример `examples-miem/lorawan`. В 234 аудитории установлен шлюз LoRaWAN, работающий с сетевым сервером Chirpstack, веб-интерфейс сетевого сервера доступен по адресу https://iotlab.auditory.ru; для получения реквизитов доступа обратитесь к преподавателю.

Пример построения сети 6LoWPAN поверх BLE из нескольких устройств на базе микроконтроллеров nRF52 (отладочные платы nRF52-DK или unwd-nrf) будет показан на одном из практических занятий.

Задания, не требующие работы непосредственно с "физическим" оборудованием, можно отлаживать и даже сдавать, используя FIT IoT-LAB (https://www.iot-lab.info/). Обратите внимание, что лаборатория расположена во Франции и для работы с LoRaWAN (используя The Things Network) нужно использовать "европейский" частотный план.

18, 19 и 20 задания из предыдущего набора еще принимаются.

## Задания

1. (1) Спецификация LoRaWAN требует, чтобы интервалы между повторными попытками передачи данных или JoinRequest выбирались случайным образом. Добавьте эти возможности в приложение.

1. (2) Сформируйте пакет, выводящий из строя устройства со старой версий Riot (посмотрите содержимое коммита `fffe8bb7328a61ab9756b28089c4f987a7f46f53`, из него должно быть ясно, в чем проблема).

1. (1) Skald - транслируйте с nRF52-DK Bluetooth-маячки с какой-то полезной информацией. (2) На другом устройстве сканируйте эфир (используйте NimBLE) и определяйте, какой из маячков ближе (его сигнал принимается с бОльшим RSSI).

1. (2) Реализуйте профиль BLE "Cycling speed and cadence", подсчитывая число импульсов на одном из входов GPIO (или любой другой на ваш выбор, кроме датчика ЧСС) с использованием библиотеки NimBLE. Вам может пригодиться пример `examples/nimble_heart_rate_sensor`.

1. (2) CoAP - соедините две или три отладочных платы nRF52-DK в сеть 6LoWPAN поверх BLE (например, используя модуль NimBLE autoconn). Запустите на одной из плат сервер, а на другой клиент CoAP и продемонстрируйте обмен сообщениями.

1. (2-...) Добавьте работу с радиосетью (LoRaWAN или 6LoWPAN поверх BLE) к любому из устройств в первом и втором блоках заданий (светофор, сейф, датчики, ...). Дополнительные баллы начисляются за оригинальность и обоснованность принятых при разработке решений (например, транслирующий свое состояние BLE-маячками светофор - устройство довольно бессмысленное, если вы меня не переубедите - а светофор, расписание работы которого передается от центра управления дорожным движением по LoRaWAN - уже вполне разумная штука). Кроме того, можно использовать любые дополнительные внешние устройства (например: кодовый замок со считывателем смарт-карт и кода с клавиатуры, имеющий возможность обновления списка "разрешенных" карт и значения кода по радио - рекомендуется LoRaWAN, а кроме того, сообщающий серверу сети о всех попытках "входа" - вполне можно оценить баллов этак на 5, если вся заявленная функциональность нормально работает).

1. (2) Описана "атака" на автосигнализацию со счетчиком переданных сообщений, в которой злоумышленник имеет возможность глушить передачи данных от брелка, а также записывать и воспроизводить их (например, здесь: https://www.drive2.ru/b/957013/). Представьте себе аналогично устроенный "умный замок" для LoRaWAN - открывающийся, например, при получении пакета с заранее определенным payload (например, четыре байта "open"). Подвержен ли он подобной атаке? Если нет - объясните, почему, если да - продемонстрируйте устройство, осуществляющее аналогичные действия.

1. (2) Центральный избирательный комитет республики Анчурия хочет разработать пейджер для голосований. Вся Анчурия покрыта сетью LoRaWAN, поэтому пейджер должен быть устройством класса C, принимающим по LoRaWAN вынесенный на голосование вопрос, выводящим его на символьный экран (можно использовать HD44780) и отправляющий выбор пользователя - одну из 4 нажатых кнопок (больше 4 кандидатов тут не бывает) - в ЦИК по LoRaWAN. Реализуйте такое устройство. (3) Реализуйте в вашем устройстве поддержку протокола тайного голосования Хе-Су с использованием криптографической библиотеки NaCl ("московский" протокол дистанционного электронного голосования).

1. (3) Реализуйте систему "умного дома" с использованием 6LoWPAN и CoAP. Поддерживаемые устройства должны включать управление освещением (светодиодами на отладочной плате), кнопочные выключатели, датчики температуры и освещенности. "Центральным контролером" в системе может быть либо устройство на базе микроконтроллера, либо компьютер, подключенный к этому микроконтроллеру. Продемонстрируйте работу каких-нибудь разумных сценариев, задействующих несколько устройств.

1. (2) В модуле LoRaWAN для операционной системы mbed отсутствует поддержка частотного плана RU864. Добавьте ее. (10) Добейтесь принятия ваших изменений в upstream.
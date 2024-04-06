---
nav_exclude: true
---

# Date format characters

WebhookScript uses the ISO format for converting and formatting dates, and the format is compatible with the [Moment.js format method](https://momentjs.com/docs/#/parsing/string-format/).

The following examples are based on the date `2017-01-05 17:04:05.084512`.

| Code      | Example       | Description                                                                                                                                       |
|-----------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| OD        | 5             | Day number with alternative numbers such as 三 for 3 if locale is ja_JP                                                                           |
| OM        | 1             | Month number with alternative numbers such as ၀၂ for 2 if locale is my_MM                                                                         |
| OY        | 2017          | Year number with alternative numbers such as ۱۹۹۸ for 1998 if locale is fa                                                                        |
| OH        | 17            | 24-hours number with alternative numbers such as ႑႓ for 13 if locale is shn_MM                                                                    |
| Oh        | 5             | 12-hours number with alternative numbers such as 十一 for 11 if locale is lzh_TW                                                                  |
| Om        | 4             | Minute number with alternative numbers such as ୫୭ for 57 if locale is or                                                                          |
| Os        | 5             | Second number with alternative numbers such as 十五 for 15 if locale is ja_JP                                                                     |
| D         | 5             | Day of month number (from 1 to 31)                                                                                                                |
| DD        | 05            | Day of month number with trailing zero (from 01 to 31)                                                                                            |
| Do        | 5th           | Day of month with ordinal suffix (from 1st to 31th), translatable                                                                                 |
| d         | 4             | Day of week number (from 0 (Sunday) to 6 (Saturday))                                                                                              |
| dd        | Th            | Minified day name (from Su to Sa), transatable                                                                                                    |
| ddd       | Thu           | Short day name (from Sun to Sat), transatable                                                                                                     |
| dddd      | Thursday      | Day name (from Sunday to Saturday), transatable                                                                                                   |
| DDD       | 5             | Day of year number (from 1 to 366)                                                                                                                |
| DDDD      | 005           | Day of year number with trailing zeros (3 digits, from 001 to 366)                                                                                |
| DDDo      | 5th           | Day of year number with ordinal suffix (from 1st to 366th), translatable                                                                          |
| e         | 4             | Day of week number (from 0 (Sunday) to 6 (Saturday)), similar to "d" but this one is translatable (takes first day of week of the current locale) |
| E         | 4             | Day of week number (from 1 (Monday) to 7 (Sunday))                                                                                                |
| H         | 17            | Hour from 0 to 23                                                                                                                                 |
| HH        | 17            | Hour with trailing zero from 00 to 23                                                                                                             |
| h         | 5             | Hour from 0 to 12                                                                                                                                 |
| hh        | 05            | Hour with trailing zero from 00 to 12                                                                                                             |
| k         | 17            | Hour from 1 to 24                                                                                                                                 |
| kk        | 17            | Hour with trailing zero from 01 to 24                                                                                                             |
|     L     | 04/09/1986                         | Date (in local format)                                                                                                       |
|    LL     | September 4 1986                   | Month name, day of month, year                                                                                               |
|   LLL     | September 4 1986 8:30 PM           | Month name, day of month, year, time                                                                                         |
|  LLLL     | Thursday, September 4 1986 8:30 PM | Day of week, month name, day of month, year, time                                                                            |
|    LT     | 8:30 PM                            | Time (without seconds)                                                                                                       |
|   LTS     | 8:30:00 PM                         | Time (with seconds)                                                                                                          |
| m         | 4             | Minute from 0 to 59                                                                                                                               |
| mm        | 04            | Minute with trailing zero from 00 to 59                                                                                                           |
| a         | pm            | Meridiem am/pm                                                                                                                                    |
| A         | PM            | Meridiem AM/PM                                                                                                                                    |
| s         | 5             | Second from 0 to 59                                                                                                                               |
| ss        | 05            | Second with trailing zero from 00 to 59                                                                                                           |
| S         | 0             | Second tenth                                                                                                                                      |
| SS        | 08            | Second hundredth (on 2 digits with trailing zero)                                                                                                 |
| SSS       | 084           | Millisecond (on 3 digits with trailing zeros)                                                                                                     |
| SSSS      | 0845          | Second ten thousandth (on 4 digits with trailing zeros)                                                                                           |
| SSSSS     | 08451         | Second hundred thousandth (on 5 digits with trailing zeros)                                                                                       |
| SSSSSS    | 084512        | Microsecond (on 6 digits with trailing zeros)                                                                                                     |
| SSSSSSS   | 0845120       | Second ten millionth (on 7 digits with trailing zeros)                                                                                            |
| SSSSSSSS  | 08451200      | Second hundred millionth (on 8 digits with trailing zeros)                                                                                        |
| SSSSSSSSS | 084512000     | Nanosecond (on 9 digits with trailing zeros)                                                                                                      |
| M         | 1             | Month from 1 to 12                                                                                                                                |
| MM        | 01            | Month with trailing zero from 01 to 12                                                                                                            |
| MMM       | Jan           | Short month name, translatable                                                                                                                    |
| MMMM      | January       | Month name, translatable                                                                                                                          |
| Mo        | 1st           | Month with ordinal suffix from 1st to 12th, translatable                                                                                          |
| Q         | 1             | Quarter from 1 to 4                                                                                                                               |
| Qo        | 1st           | Quarter with ordinal suffix from 1st to 4th, translatable                                                                                         |
| G         | 2017          | ISO week year (see ISO week date)                                                                                                                 |
| GG        | 2017          | ISO week year (on 2 digits with trailing zero)                                                                                                    |
| GGG       | 2017          | ISO week year (on 3 digits with trailing zeros)                                                                                                   |
| GGGG      | 2017          | ISO week year (on 4 digits with trailing zeros)                                                                                                   |
| GGGGG     | 02017         | ISO week year (on 5 digits with trailing zeros)                                                                                                   |
| g         | 2017          | Week year according to locale settings, translatable                                                                                              |
| gg        | 2017          | Week year according to locale settings (on 2 digits with trailing zero), translatable                                                             |
| ggg       | 2017          | Week year according to locale settings (on 3 digits with trailing zeros), translatable                                                            |
| gggg      | 2017          | Week year according to locale settings (on 4 digits with trailing zeros), translatable                                                            |
| ggggg     | 02017         | Week year according to locale settings (on 5 digits with trailing zeros), translatable                                                            |
| W         | 1             | ISO week number in the year (see ISO week date)                                                                                                   |
| WW        | 01            | ISO week number in the year (on 2 digits with trailing zero)                                                                                      |
| Wo        | 1st           | ISO week number in the year with ordinal suffix, translatable                                                                                     |
| w         | 1             | Week number in the year according to locale settings, translatable                                                                                |
| ww        | 01            | Week number in the year according to locale settings (on 2 digits with trailing zero)                                                             |
| wo        | 1st           | Week number in the year according to locale settings with ordinal suffix, translatable                                                            |
| x         | 1483635845085 | Millisecond-precision timestamp (same as date.getTime() in JavaScript)                                                                            |
| X         | 1483635845    | Timestamp (number of seconds since 1970-01-01)                                                                                                    |
| Y         | 2017          | Full year from -9999 to 9999                                                                                                                      |
| YY        | 17            | Year on 2 digits from 00 to 99                                                                                                                    |
| YYYY      | 2017          | Year on 4 digits from 0000 to 9999                                                                                                                |
| YYYYY     | 02017         | Year on 5 digits from 00000 to 09999                                                                                                              |
| YYYYYY    | +002017       | Year on 5 digits with sign from -09999 to +09999                                                                                                  |
| z         | UTC           | Abbreviated time zone name                                                                                                                        |
| zz        | UTC           | Time zone name                                                                                                                                    |
| Z         | +00:00        | Time zone offset HH:mm                                                                                                                            |
| ZZ        | +0000         | Time zone offset HHmm                                                                                                                             |

Source: [Carbon Docs](https://carbon.nesbot.com/docs/#api-localization)

# Timezone List

* Africa/Abidjan
* Africa/Accra
* Africa/Addis_Ababa
* Africa/Algiers
* Africa/Asmara
* Africa/Bamako
* Africa/Bangui
* Africa/Banjul
* Africa/Bissau
* Africa/Blantyre
* Africa/Brazzaville
* Africa/Bujumbura
* Africa/Cairo
* Africa/Casablanca
* Africa/Ceuta
* Africa/Conakry
* Africa/Dakar
* Africa/Dar_es_Salaam
* Africa/Djibouti
* Africa/Douala
* Africa/El_Aaiun
* Africa/Freetown
* Africa/Gaborone
* Africa/Harare
* Africa/Johannesburg
* Africa/Juba
* Africa/Kampala
* Africa/Khartoum
* Africa/Kigali
* Africa/Kinshasa
* Africa/Lagos
* Africa/Libreville
* Africa/Lome
* Africa/Luanda
* Africa/Lubumbashi
* Africa/Lusaka
* Africa/Malabo
* Africa/Maputo
* Africa/Maseru
* Africa/Mbabane
* Africa/Mogadishu
* Africa/Monrovia
* Africa/Nairobi
* Africa/Ndjamena
* Africa/Niamey
* Africa/Nouakchott
* Africa/Ouagadougou
* Africa/Porto-Novo
* Africa/Sao_Tome
* Africa/Tripoli
* Africa/Tunis
* Africa/Windhoek
* America/Adak
* America/Anchorage
* America/Anguilla
* America/Antigua
* America/Araguaina
* America/Argentina/Buenos_Aires
* America/Argentina/Catamarca
* America/Argentina/Cordoba
* America/Argentina/Jujuy
* America/Argentina/La_Rioja
* America/Argentina/Mendoza
* America/Argentina/Rio_Gallegos
* America/Argentina/Salta
* America/Argentina/San_Juan
* America/Argentina/San_Luis
* America/Argentina/Tucuman
* America/Argentina/Ushuaia
* America/Aruba
* America/Asuncion
* America/Atikokan
* America/Bahia
* America/Bahia_Banderas
* America/Barbados
* America/Belem
* America/Belize
* America/Blanc-Sablon
* America/Boa_Vista
* America/Bogota
* America/Boise
* America/Cambridge_Bay
* America/Campo_Grande
* America/Cancun
* America/Caracas
* America/Cayenne
* America/Cayman
* America/Chicago
* America/Chihuahua
* America/Costa_Rica
* America/Creston
* America/Cuiaba
* America/Curacao
* America/Danmarkshavn
* America/Dawson
* America/Dawson_Creek
* America/Denver
* America/Detroit
* America/Dominica
* America/Edmonton
* America/Eirunepe
* America/El_Salvador
* America/Fort_Nelson
* America/Fortaleza
* America/Glace_Bay
* America/Goose_Bay
* America/Grand_Turk
* America/Grenada
* America/Guadeloupe
* America/Guatemala
* America/Guayaquil
* America/Guyana
* America/Halifax
* America/Havana
* America/Hermosillo
* America/Indiana/Indianapolis
* America/Indiana/Knox
* America/Indiana/Marengo
* America/Indiana/Petersburg
* America/Indiana/Tell_City
* America/Indiana/Vevay
* America/Indiana/Vincennes
* America/Indiana/Winamac
* America/Inuvik
* America/Iqaluit
* America/Jamaica
* America/Juneau
* America/Kentucky/Louisville
* America/Kentucky/Monticello
* America/Kralendijk
* America/La_Paz
* America/Lima
* America/Los_Angeles
* America/Lower_Princes
* America/Maceio
* America/Managua
* America/Manaus
* America/Marigot
* America/Martinique
* America/Matamoros
* America/Mazatlan
* America/Menominee
* America/Merida
* America/Metlakatla
* America/Mexico_City
* America/Miquelon
* America/Moncton
* America/Monterrey
* America/Montevideo
* America/Montserrat
* America/Nassau
* America/New_York
* America/Nipigon
* America/Nome
* America/Noronha
* America/North_Dakota/Beulah
* America/North_Dakota/Center
* America/North_Dakota/New_Salem
* America/Nuuk
* America/Ojinaga
* America/Panama
* America/Pangnirtung
* America/Paramaribo
* America/Phoenix
* America/Port-au-Prince
* America/Port_of_Spain
* America/Porto_Velho
* America/Puerto_Rico
* America/Punta_Arenas
* America/Rainy_River
* America/Rankin_Inlet
* America/Recife
* America/Regina
* America/Resolute
* America/Rio_Branco
* America/Santarem
* America/Santiago
* America/Santo_Domingo
* America/Sao_Paulo
* America/Scoresbysund
* America/Sitka
* America/St_Barthelemy
* America/St_Johns
* America/St_Kitts
* America/St_Lucia
* America/St_Thomas
* America/St_Vincent
* America/Swift_Current
* America/Tegucigalpa
* America/Thule
* America/Thunder_Bay
* America/Tijuana
* America/Toronto
* America/Tortola
* America/Vancouver
* America/Whitehorse
* America/Winnipeg
* America/Yakutat
* America/Yellowknife
* Antarctica/Casey
* Antarctica/Davis
* Antarctica/DumontDUrville
* Antarctica/Macquarie
* Antarctica/Mawson
* Antarctica/McMurdo
* Antarctica/Palmer
* Antarctica/Rothera
* Antarctica/Syowa
* Antarctica/Troll
* Antarctica/Vostok
* Arctic/Longyearbyen
* Asia/Aden
* Asia/Almaty
* Asia/Amman
* Asia/Anadyr
* Asia/Aqtau
* Asia/Aqtobe
* Asia/Ashgabat
* Asia/Atyrau
* Asia/Baghdad
* Asia/Bahrain
* Asia/Baku
* Asia/Bangkok
* Asia/Barnaul
* Asia/Beirut
* Asia/Bishkek
* Asia/Brunei
* Asia/Chita
* Asia/Choibalsan
* Asia/Colombo
* Asia/Damascus
* Asia/Dhaka
* Asia/Dili
* Asia/Dubai
* Asia/Dushanbe
* Asia/Famagusta
* Asia/Gaza
* Asia/Hebron
* Asia/Ho_Chi_Minh
* Asia/Hong_Kong
* Asia/Hovd
* Asia/Irkutsk
* Asia/Jakarta
* Asia/Jayapura
* Asia/Jerusalem
* Asia/Kabul
* Asia/Kamchatka
* Asia/Karachi
* Asia/Kathmandu
* Asia/Khandyga
* Asia/Kolkata
* Asia/Krasnoyarsk
* Asia/Kuala_Lumpur
* Asia/Kuching
* Asia/Kuwait
* Asia/Macau
* Asia/Magadan
* Asia/Makassar
* Asia/Manila
* Asia/Muscat
* Asia/Nicosia
* Asia/Novokuznetsk
* Asia/Novosibirsk
* Asia/Omsk
* Asia/Oral
* Asia/Phnom_Penh
* Asia/Pontianak
* Asia/Pyongyang
* Asia/Qatar
* Asia/Qostanay
* Asia/Qyzylorda
* Asia/Riyadh
* Asia/Sakhalin
* Asia/Samarkand
* Asia/Seoul
* Asia/Shanghai
* Asia/Singapore
* Asia/Srednekolymsk
* Asia/Taipei
* Asia/Tashkent
* Asia/Tbilisi
* Asia/Tehran
* Asia/Thimphu
* Asia/Tokyo
* Asia/Tomsk
* Asia/Ulaanbaatar
* Asia/Urumqi
* Asia/Ust-Nera
* Asia/Vientiane
* Asia/Vladivostok
* Asia/Yakutsk
* Asia/Yangon
* Asia/Yekaterinburg
* Asia/Yerevan
* Atlantic/Azores
* Atlantic/Bermuda
* Atlantic/Canary
* Atlantic/Cape_Verde
* Atlantic/Faroe
* Atlantic/Madeira
* Atlantic/Reykjavik
* Atlantic/South_Georgia
* Atlantic/St_Helena
* Atlantic/Stanley
* Australia/Adelaide
* Australia/Brisbane
* Australia/Broken_Hill
* Australia/Darwin
* Australia/Eucla
* Australia/Hobart
* Australia/Lindeman
* Australia/Lord_Howe
* Australia/Melbourne
* Australia/Perth
* Australia/Sydney
* Europe/Amsterdam
* Europe/Andorra
* Europe/Astrakhan
* Europe/Athens
* Europe/Belgrade
* Europe/Berlin
* Europe/Bratislava
* Europe/Brussels
* Europe/Bucharest
* Europe/Budapest
* Europe/Busingen
* Europe/Chisinau
* Europe/Copenhagen
* Europe/Dublin
* Europe/Gibraltar
* Europe/Guernsey
* Europe/Helsinki
* Europe/Isle_of_Man
* Europe/Istanbul
* Europe/Jersey
* Europe/Kaliningrad
* Europe/Kiev
* Europe/Kirov
* Europe/Lisbon
* Europe/Ljubljana
* Europe/London
* Europe/Luxembourg
* Europe/Madrid
* Europe/Malta
* Europe/Mariehamn
* Europe/Minsk
* Europe/Monaco
* Europe/Moscow
* Europe/Oslo
* Europe/Paris
* Europe/Podgorica
* Europe/Prague
* Europe/Riga
* Europe/Rome
* Europe/Samara
* Europe/San_Marino
* Europe/Sarajevo
* Europe/Saratov
* Europe/Simferopol
* Europe/Skopje
* Europe/Sofia
* Europe/Stockholm
* Europe/Tallinn
* Europe/Tirane
* Europe/Ulyanovsk
* Europe/Uzhgorod
* Europe/Vaduz
* Europe/Vatican
* Europe/Vienna
* Europe/Vilnius
* Europe/Volgograd
* Europe/Warsaw
* Europe/Zagreb
* Europe/Zaporozhye
* Europe/Zurich
* Indian/Antananarivo
* Indian/Chagos
* Indian/Christmas
* Indian/Cocos
* Indian/Comoro
* Indian/Kerguelen
* Indian/Mahe
* Indian/Maldives
* Indian/Mauritius
* Indian/Mayotte
* Indian/Reunion
* Pacific/Apia
* Pacific/Auckland
* Pacific/Bougainville
* Pacific/Chatham
* Pacific/Chuuk
* Pacific/Easter
* Pacific/Efate
* Pacific/Fakaofo
* Pacific/Fiji
* Pacific/Funafuti
* Pacific/Galapagos
* Pacific/Gambier
* Pacific/Guadalcanal
* Pacific/Guam
* Pacific/Honolulu
* Pacific/Kanton
* Pacific/Kiritimati
* Pacific/Kosrae
* Pacific/Kwajalein
* Pacific/Majuro
* Pacific/Marquesas
* Pacific/Midway
* Pacific/Nauru
* Pacific/Niue
* Pacific/Norfolk
* Pacific/Noumea
* Pacific/Pago_Pago
* Pacific/Palau
* Pacific/Pitcairn
* Pacific/Pohnpei
* Pacific/Port_Moresby
* Pacific/Rarotonga
* Pacific/Saipan
* Pacific/Tahiti
* Pacific/Tarawa
* Pacific/Tongatapu
* Pacific/Wake
* Pacific/Wallis
* UTC

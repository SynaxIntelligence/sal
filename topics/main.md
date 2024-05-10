# Главная

Документ применяется в рамках реализации проекта **%project_full_name%**.

<available-only-for instance="ms-2.0">
    <include from="wlibs.md" element-id="generic-warning"> <var name="latest" value="1.7"/>
    </include>
</available-only-for>

## Продукт

Основная цель продукта - помочь пользователям максимально эффективно спланировать свое посещение музея, учитывая их интересы, предпочтения и доступные ресурсы.
Для достижения этой цели приложение предоставляет следующие основные функции:

1. **Авторизация через аккаунты в социальных сетях**: Пользователи могут авторизоваться в приложении, используя свои учетные записи в популярных социальных сетях, таких как VK, Google и др.
2. **Планирование посещения музея**: Пользователи могут указать город, музей, дату и время своего планируемого посещения.
3. **Получение информации о музее**: Приложение предоставляет информацию о режиме работы музея, его веб-сайте, адресе и других важных деталях.
4. **Прикрепление билетов к посещению**: Пользователи могут прикрепить билеты к своему планируемому посещению музея.
5. **Создание чек-листа / заметки о посещении**: Пользователи могут создавать чек-листы или заметки о том, какие залы и экспонаты они хотят посетить в музее.
6. **Просмотр ленты новостей о новых выставках**: Пользователи могут получать информацию о новых выставках, проходящих в музеях, и быть в курсе последних новостей из мира искусства. 

Эти функции обеспечивают удобство и эффективность в планировании посещений музеев, делая приложение полезным инструментом для любителей искусства и культуры.

## Контекст

Суть приложения заключается в создании удобной платформы для планирования и организации посещения музеев и выставок.
Пользователи могут использовать приложение для составления списков интересующих их произведений искусства, планирования походов в музеи и получения полезной информации о местах, которые они собираются посетить.

## Бизнес-специфика

Бизнес-специфика приложения направлена на обеспечение удовлетворения потребностей пользователей в организации культурных мероприятий и создании ценности для различных сторон — от пользователей и музеев до партнеров и инвесторов.
**Ниже представлены основные аспекты бизнес-специфики приложения:**

1. **Удобство и простота использования**: Приложение должно быть интуитивно понятным и легким в использовании для широкого круга пользователей, включая как опытных пользователей мобильных приложений, так и тех, кто не имеет опыта в данной области.
2. **Персонализация**: Приложение должно предоставлять возможность персонализации опыта пользователей в соответствии с их предпочтениями и интересами в искусстве и культуре.
3. **Партнерство с музеями и галереями**: Сотрудничество с различными музеями и галереями для обеспечения актуальной информации о выставках, расписании работы и доступности билетов.
4. **Монетизация**: Возможные источники дохода могут включать в себя продажу билетов на выставки через приложение, партнерские программы с музеями, рекламу культурных событий и товаров, а также премиум-подписку с дополнительными функциями.
5. **Аналитика и отзывы пользователей**: Сбор и анализ данных об использовании приложения, отзывов и предпочтений пользователей для постоянного улучшения и развития функциональности приложения.
6. **Масштабирование**: Возможность расширения географического охвата и добавления новых функций для привлечения большего числа пользователей и обеспечения роста бизнеса.

## Контекстная диаграмма

Данная диаграмма описывает внешние взаимодействия ИС и представляет общую верхнеуровневую архитектуру решения.

### Системы и внешние системы:
- **Museum System:** Система предоставления доступа к информации музея.
- **Google System и VK System:** Внешние системы, взаимодействующие с приложением через REST API.

### App Layer:
- **Mobile App:** Интерфейс взаимодействия с пользователями мобильного приложения, реализованный с использованием React Native.
- **API Application:** Агрегация API интерфейсов сервисов, реализованных на Java и упакованных в Docker контейнер.
- **База данных:** Включает служебную базу данных для управления конфигурациями и API, реализованную с помощью PostgreSQL.

### Микросервисы:
- **AuthService, UserService, MuseumService, VisitService, RouteService:** Микросервисы, ответственные за аутентификацию, управление пользователями, работу с музеями, посещениями и маршрутами соответственно.

### Очереди и базы данных:
- **Message Bus:** RabbitMQ, используемый для обмена сообщениями между микросервисами.
- **Базы данных пользователей, маршрутов, посещений и музеев:** Различные базы данных, используемые для хранения данных, такие как Postgre SQL, MS SQL и Oracle SQL.

### Взаимодействия:
- Взаимодействие между контейнерами и внешними системами происходит через различные протоколы, такие как HTTPS, XML и AMQP 0-9-1.
- Взаимодействие между микросервисами осуществляется синхронно и асинхронно через JSON/HTTPS и XML/HTTPS.

> [Сервер](https://www.plantuml.com/plantuml/uml/jLZhRXf75FxFKqn9f81a6pjE8ZKgaJ3Gn2ct04dQNsZOdS2MlMLtm45LfLpQD9LQfPKYjRzQLNq19waROZVa5POtwZapk-okmGRSr1UOozdpdNFct6Ola8yqKz7xAYDTpcttQYRZqBsDZiQx_NRVPOvYcPoPV4EnZ8ojKvFt3NtTvQgkjJFvI-irNBfTBcKCwdBcm58h3qzGpMJEXWsqYId_JvHBizlN8lkyRrFLsSweRA01h9jn65NugHHVqW4zbS2sNDvnc7jVNmnd3tdNCXVJgHOt6L-6JkajewO1qhN0r8DJYE-1rTRf7dCjWsNmNDo5L9BZGZ9c3fXksUnQ8l6Hokx1oP12ySvklbffBE4I0SkfQw1AwmB0jHsDCpVmZ43TASgdrKepTxVOg9QB7nGegjtwvKJYWgjGdP7DZIqSzpJJfWurY0uoyA7DYEN0iS_TiIrzY9D4kBVdKFkkfl8kkRYvcKXmZGDhxuKtylQzrvE7yFaF_EuJ-1XvXx0mdZpo3k3xbJU2qTXxHRmHWTaxM7q6dwF9jpXz0q-EuA6nzvTtuBsTF9eynaUyjqGileJXqUG7e1zxhxqnyTu3IrY2wTz0ZsoUWtQbt1VLsytMtTtcZLQfUBrOAQJIqzLIhb9ev7Er8gmrRbJljch5UgDQQTMgzMOzjzk4vKHELOiwCy3eJTf99GrDSQm6-96ciEGQEIyjdKrYsAq9isQtn7gNgjQUPdQoIUxqcRzaisnHwtHvGrEPsi1vAWqxEkimKsso1pmh0OWh4KYA8JbnaJvDKgP5E52j4HYqgT8ZYgLRJZgPFYucRWBBQMP1VFI2FD9dpnTBnNAnqcoXmxNorLAr3lljZjnDdjlUlbp8NLvUPX-DA05SNEvPyLnkERGJiKhTwfj0kcCz216cykW2lZVSqQKXGqMIRHsWP_dVxpD9EkL1TJ1d-oG6I6avAdFyLPKwFSYHmt2ZsTMKdibSDvkyc9HkKMUw0AFkq5IG4e_6Dt2kNWTtYfaNmoQs6zrey25uJe6wNQQMO9vAfwCGY93vW3WMvo5E8b63v6cPAKmmQoJf_GunXA7r1eFJsuUuEy1vyiGzZDzbOp8QD29hWpLzVAeQceaWFq78OxR01o3iCOa0q7Zo42tV649ECrh51pnb08E-qNB52ZnO5dCYAOIuVqWE02vI4Cfp0Cp7Od4VD3WAv2B1ykI9znvf3mbACFa6SV7foLEOew90y0PIrNCGnfTb1xsNEiDKnx8wEaE10Fowc0JIfCbN2G8_4V4bTKXPBpQQ95VR1SPVpx0Uz7osTpuxXUMW9obYh6PuALk-iGmDp9MpxIZ7n3Hff0ohhO4wrBQHNaoG6YrRnqQ4L2ZN1anO-bUmrMFCws0naQvFoU5WRTn_FzVFdkFHdysVH7UKbAxUooQnX485rIr8orteUgvUsTw-T37ZKhr5zxgjxIiPsu4IpFRWs-BMHfSREXWirD_FQs003LG4SwBsa4X0Qyj4hMzYrYS5qTMGQB8LnC9_uZQPANqfOOL3i1FQwXtnY-O1w3l2Mec60KN10caH-hJZPkTczsWXmZ2PRXRQAPLosgOkkbh17wACDTa9aiQjaXyiH-3RQDcN0BYFCV6pzm83umXFx8am_x6WEGGHCKX68FOJ4QXFSKEUuKYuO4IuiFUCYHXwfe4UNiOIw5T0L_eayN_2iw5ztcsvpW1j3SEm94iBI7scjWQxWdZeO7WY8o7mOH3JeM5ZrJqz1nKpbezw6uOBKUUwEFh22fX1bXEeCiL5SFFdo4Qbs9o5zlCK_BwA7e5irLU07sYkndtqEpXUHcdXvzzBDrb9MSVgS-QZrN4SGPEtaJcQWc4VJfx1FnxnEAxlzA7v4bmuuOpjBcG4_vHhE5wajIWKWBuA4bKKS7oEBYn72qtxf_VBAW1AboazNNCH8X-C5sho7PpR8LPraQzzUouBoHvqjRQ6W4KvMWZt8zmA7eb8UIVh_6g071epXdXDCLXeGb5KO65b8AmZcFY1OyaVBWGxaibTv9ctgu3vGH-ueGpx_yqHJRQ7YRS2NmjLUYTIsTXlgqvMQZQuRs5NdZAWYORUlmNtMLHCpiXEtnLj1Ms3ovHl2TZVq1FzZYsIf6LpFmy0Ifq8NhMzeDA9idPgRfvJiQO21BUNz5m9P0PRJeJJCzVAq39Lpq2N6pEAp-Rd03NowcLPMDzNPt2h3bNqunhFhqeBKAUmS26ArE3miA4TLLropx4CGk4YkYTUVn1k8J1UczR8pS9EFY8_CeeMrgWEPs8MAPEHOpWJgqWDZ3ZJqgnYlC8sAHvtDSTI-pBCS-LRDRAv_l7wLboErWwqcH5hnnc00xXzOvO1N3VWBn4S53mMlKH0EHLnBjvknJjrVDaLlCeIxxTm2nWABUJDyB-o4hoYJE8DVi2H-kPiL2kP6yrchH6wfBo3-vnYJn-_YmRCmglx6lcyN3hEC7ApbwfY1nmNgy1qk6Gvft0JJxOg-CwbRKLROt4TFACay_XDRwndvOak5J8ExoLnZPTszNy1)
> [SVG](https://www.plantuml.com/plantuml/svg/jLZlZjl64V-kfzWe0Im1ToVRPmTeK0NHIMhiL2V9acotduWLkPPOaLo6kzHPA0B4IV-aG8kqG83sKukYBt1nUhLyLyklGBrHPvRB8scUJwUhSxAb_JFx-ytCpimk-OcGD92XwvHkaFTiptH2Yv6fbBxug5OBwD7Un9RJS1mA5fZSayoJUoPtQxv3FLorAwJbsEDQyyvk7uSU7dPgBXMI1J1aD645jJqMxFd8S8x_K_DESVhZpBmCVMe5-pMBpMsW5RM0KLDUAl4hEgUN2lXSo4d0nEVEPZf_8QVSsondSUanUHKvStOLCrtGpW1NpoyHVW9UswL7J72NrN1Vn4Qf676Z6FFcpE4--xXKUizYJs1dIAlzw7wprnrU8IGqP1eQQDAk8X1-O4icaiX8p3rd-LclEseyRWzxX-rtIfIrRlTkgNH3cDHXvERUBMpFRC-d0NM90ph8XSy83s3RBvpnkRF0JYcTEmge_zYsv9JSldcpL9As1EZeksWP7KS_hB-4x__2vvZ0rp8wXO7L-bbq0h_FeoMqLj5p4Yq9z5x1w3VmlLp_5hilOEKI5gsYVqSdqSlri_LNk2HwITJWzz0yM_yHv5VH3z6AHAy14eQW-n-GHvXlmRfEuvUzXoFZyVtHFQFJ_hJTRLMgvwETHhSrR3RwRHWRtkizDlhjmR3NDVgzmMZGk3-2uLB3ijeESy7f8pgfb5tR3FYG1R1phBn3FeWzNIzZskqejzPlgV4fjVYHxKtgPHc4J0_vhDws9rCvj2rc3R5VgSACmoRCiqRigQp714J43AJ2K9m8bA-IYiU91AaT0eqnDMV4v0uFgkNgcshY942ULnRanoXeedpzWtQdVTZkZWmCEAFPw_G6C3-UnBFbz_VtxxOQTw-kisOZPaANrxkedf0ye9ECLmOyz43qW3_L35bz74K_Mnmu8SiP0imEK1VnFmyPY6Ong0Fk7ByD02LvOB50Zreqc46DNAGJewbjpZmcHBry6_YGSC0SHKR5mZDH4hT6ExWn640uvToBQPETpKqCvG8YfqN5b5aTw5UgrIm5CjJU8G-NCkKfbVei4DohO87P8UNe7z5AfTOBJCxe6FBk1Flbjyv5owldP3Pfa520DpK_jLpRGv8_GyfZjO05cFO0WaIhzPVe-U52IEOQxQUouW90w1f2ZS32GzKdiOHIzvyn0f2h4eJwd03uIWqUWmLdYLua6Lv_7Rr6sLE26gn_WxouUlqxwAEX8F0YEW5Bgeak1nYzD5XK9fnF78OA0VcdgfDeKoM_BX7uIzNNqgdae3qSaKR_FW1_KO2UppJiev-_7HAab4GUge1btjBEScrmLyFtiuYbyw9HSVdO1dEexwEywg0qUdQ05n7IfTAUC-Nflu6lliAw3XvJvVgI6WxUnldN5yRPjo1_pNWAKAbo7EgpUXcFK3X17GvbUSg5_EZ3_Vqxjsk2EWOzcXhx7zRy08vWTWI_NFAzgNITSZLZlwvhu00RJ0HtelLGIC1gxg7Lds7L9orrgo5fiTN2qRBWayBHLr5UE0K_eQzU4Nrede2zI_W54Hn63rHLwjE9g5zOtRC74HYHMj4QLomgwPWA3BMMRgAE_VWcI8OFEZfPpY2sqRFV0-4nviHVekymCSwW3LFe_dpIWEOhbIHBKFjhdCOqIVPmYI6OLIwzU-PKJ2FJ5HXfU0Jg4r34CKdqNxetD9HJGmHpz3KqqoDPUI2s9_Kr-1NKmm337LagXK-Jd4uTcplTgqLMLI8rwqDeRcIzCCGn5hRWr5KEMPCIb-5jla_skkrHaLhNAVWypsv1V5NVWdvk2rjgzaVOlehHAix_48V9LiO6F9HCimsmdM6BdqQAV52S8SM-WV-unQkSlUcYYpMuyPOzzgTSShtBVMnliXeF2cJVXecQ9WI-n11MhSsk_LVqrsq8p2apPuujaAAPj3TQydlOjzFe33lQdrjGigTJUsmZOLkrDjFz2PuAdc7GOD7Pdb3QK0oHRuIDZNJneG83MnCvF2xyWDZHpOraU5GbTURbDcGwwNKOwhJ_qGBHOqTOUBlmiz6aL-WtVOEwh90La_i1tiehBXE2JfWn3bMjZtla81H8DQ1Z29d31uhsxnY9-iQMAT9ukR-Oe3MEazSQRpZfu5ZRK9kB9rQgGFBqKhrG0rN1hgJ2XigrFRKgrKNgms6UjLYVCwoPLozNfTMnMk3j1THqyXPdJwKjMCzf1yp9dC7fPWyOjGHv4d2NKCyYHuWgYEH8Z8zDE-Ipra4JaB90sODLjwyFbZacLVFwKDapK3MtXCfYPQv9-Rph1zmAupHl73xeavkxFzczbTV3EA3cJ7kx200184At2F152V-Laes2PTc723XELPwhjrlvcpg-x4fUPQdtMpW5W8YadWp_VoY5bGN9Nl1JHAhTEUnrQ_T6e_um3KarbI3bLkUUHLEmzD4T47zns7aJC9tMfhhYJRLQpB4XBov1KokDBhvp6VFirNW-kxuc5-7f9zRhOs98fS3fSqd6ucr2_HDO0tlyFm00)

<code-block lang="plantuml" src="../diagrams/c4.puml" >

</code-block>

## Результат

Реализована спецификация требований на разработку мобильного приложения, которое предоставляет следующую функциональность:
-	авторизация через аккаунты в социальных сетях
-	возможность планирования посещения музея (город, музей, дата, время) 
-	получение информации о музее (режим работы, сайт, адрес)
-	возможность прикрепить билеты к посещению
-	возможность создать чек-лист/заметку о посещении (какие залы нужно посетить, какие экспонаты посмотреть) 
-	возможность посмотреть ленту новостей о новых выставках

## Дорожная карта проекта

<code-block lang="plantuml" src="../diagrams/roadmap.puml">


</code-block>

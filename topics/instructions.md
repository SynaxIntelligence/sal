# Инструкции

## Загрузить справочники

<a href="http://172.30.48.97/api/nsi/docs/swagger-ui/index.html#/" alt="rest api">REST API спецификация</a>

### 1. Загрузить атрибуты целевого справочника в справочник SPR_REC

> *endpoint GET api/nsi/directory/data/import*

- [ ] В параметрах запроса передать код справочника SPR_REC

- [ ] В теле запроса передать файл Excel с перечнем атрибутов

> **Важная информация**
>
> SPR_REC обязательно должен быть с ид 1.
> Указывается код справочника куда - целевого
>
{style="note"}


### 2. **Загрузить данные справочника**

    Контроллер - directory-controller

    через json - 

    протестить status - попробовать вызвать скрытый справочник

### 3. **Загрузить строки**

    Контроллер directory-excel

    Код справочника

## Развернуть приложение через docker compose

<procedure title="Процедура" id="процедура" collapsible="true" default-state="collapsed">
<step>Выполнить миграции (restore from dump)</step>
<step>Настроить хосты
</step>
<step>В проекте 1147_config cloud-auth-server-local.yml: прописать настройки ldap.
</step>
<step>В проект 1147_front в файле webpack.config.js прописать target: http://eksc-gateway:8093/{}</step>
<step>Перейти в директорию с docker-compose.yml</step>
<step>Запустить VM AD</step>
<step>Проверить действие всех сертификатов в сервисе back</step>
<step>Приложение доступно на localhost:8000</step>
</procedure>

<tldr>
   <p>ipconfig - проверить ip (заменить 192.168.1.67)</p>
   <p>Docker</p>
   <p>192.168.1.67 host.docker.internal</p>
   <p>192.168.1.67 gateway.docker.internal</p>
   <p>Nexus 192.168.1.67 nexus.local</p>
   <p>AD 192.168.109.128 (проверить ip в vm) WIN-I9R1ILE7GN7.vkd.local</p>
</tldr>

## Настроить LDAP сервер {id="ldap_1"}

<note>
    <p>Указать корректный порт LDAP.</p>
    <p> 3268 - General Catalogue port (GC) used only for LDAP reads</p>
    <p> 398 - insecure connection</p>
    <p> 636 - SSL connections (needs a valid certificate)</p>    
</note>

<tip>
    <p>
        Справка по настройкам LDAP сервера на Windows AD.         
    </p>
   <p>
    <a href="https://learn.microsoft.com/en-us/answers/questions/756667/https://learn.microsoft.com/en-us/answers/questions/756667/access-denied-and-active-directory-operation-faile" alt="LDAP settings">LDAP настройки</a>
   </p>
</tip>

<tabs>
<tab title="Настройка сервиса auth">
<code-block lang="yaml" collapsed-title="cloud-auth-server-local.yml" collapsible="true" default-state="collapsed">
   ldap:
      url: ldap://WIN-I9R1ILE7GN7.vkd.local:3268/
      group-search-base: DC=vkd,DC=local
      user:
      search-base: DC=vkd,DC=local
      manager-dn: CN=eksc_ldap,OU=eksc,DC=vkd,DC=local
      manager-password: Password4
      port: 3268
</code-block>
</tab>
<tab title="Настройка сервиса back">
<code-block lang="yaml" collapsed-title="docs-service-local.yml" collapsible="true" default-state="collapsed">
   ldap:
      url: ldap://WIN-I9R1ILE7GN7.vkd.local:3268/
      group-search-base: DC=vkd,DC=local
      user:
      search-base: DC=vkd,DC=local
      manager-dn: CN=eksc_ldap,OU=eksc,DC=vkd,DC=local
      manager-password: Password4
      port: 3268
</code-block>
</tab>
<tab title="Настройка сервиса mail">
<code-block lang="yaml" collapsed-title="mail-service-local.yml" collapsible="true" default-state="collapsed">
  mail:
     host: mail.sibintek.ru
     port: 465
     protocol: smtp
     username: rodos@sibintek.ru
     password: "!b?Mwx$bP^gmD2NyMMs!ZfK3YYfQq5y*%QNu7rsCsuU#Ct"
     usernamefrom: rodos@sibintek.ru
     properties.mail.smtp.auth: true
     properties.mail.smtp.starttls.enable: false
     properties.mail.smtp.starttls.required: false
     properties.mail.smtp.timeout: 10000
     properties.mail.smtp.connectiontimeout: 10000
</code-block>
</tab>
</tabs>

#### Порядок запуска контейнеров
```Bash 
docker-compose run -d -p 8081:8081 --name nexus-local --build nexus-local
docker-compose run -d -p 8888:8888 --name eksc-config --build eksc-config
docker-compose run -d -p 8761:8761 --name eksc-discovery --build eksc-discovery
docker-compose run -d -p 8093:8093 --name eksc-gateway --build eksc-gateway
```

#### Notes:
when directory-service cannot find eksc-redis - change eksc-redis to host.docker.internal in application-build.yml
as well as eksc-postgres

---
## LDAP

1. The App user (in config) should be part of Domain Admins Group\
2. Use unicodePwd property to write new user
3. Different dbs referenced from auth-service config and back-service config
4. Updated users table id to autoincrement

<tip>
    <p>
        Коды доступов User Account в Windows AD         
    </p>
   <p>
    <a href="https://winitpro.ru/index.php/2018/05/14/convertaciya-atributa-useraccountcontrol-v-ad" alt="LDAP settings">LDAP настройки</a>
   </p>
</tip>



## Конфигурации proxy серверов

<tabs>
<tab title="Конфигурация для сервиса event sourcing (sse)">
<code-block lang="nginx" collapsible="true" default-state="collapsed">
proxy_set_header Connection '';
proxy_http_version 1.1;
chunked_transfer_encoding off; 
proxy_buffering off;
proxy_cache off;
</code-block>
</tab>
</tabs>


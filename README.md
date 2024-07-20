# Домашнее задание к занятию 9 «Процессы CI/CD» - `Мурчин Артем`

## Подготовка к выполнению

1. Создайте два VM в Yandex Cloud с параметрами: 2CPU 4RAM Centos7 (остальное по минимальным требованиям).
2. Пропишите в [inventory](./infrastructure/inventory/cicd/hosts.yml) [playbook](./infrastructure/site.yml) созданные хосты.
3. Добавьте в [files](./infrastructure/files/) файл со своим публичным ключом (id_rsa.pub). Если ключ называется иначе — найдите таску в плейбуке, которая использует id_rsa.pub имя, и исправьте на своё.
4. Запустите playbook, ожидайте успешного завершения.
5. Проверьте готовность SonarQube через [браузер](http://localhost:9000).
6. Зайдите под admin\admin, поменяйте пароль на свой.
7.  Проверьте готовность Nexus через [бразуер](http://localhost:8081).
8. Подключитесь под admin\admin123, поменяйте пароль, сохраните анонимный доступ.

## Решение - подготовка к выполнению

Создаа две VM в Yandex Cloud. Выполнил п. 2-3. Запустил playbook и дождался успешного завершения:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-01-hw.png)

Проверил готовность SonarQube:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-02-hw.png)

Проверил готовность Nexus:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-03-hw.png)

## Знакомоство с SonarQube

### Основная часть

1. Создайте новый проект, название произвольное.
2. Скачайте пакет sonar-scanner, который вам предлагает скачать SonarQube.
3. Сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
4. Проверьте `sonar-scanner --version`.
5. Запустите анализатор против кода из директории [example](./example) с дополнительным ключом `-Dsonar.coverage.exclusions=fail.py`.
6. Посмотрите результат в интерфейсе.
7. Исправьте ошибки, которые он выявил, включая warnings.
8. Запустите анализатор повторно — проверьте, что QG пройдены успешно.
9. Сделайте скриншот успешного прохождения анализа, приложите к решению ДЗ.

## Решение - знакомоство с SonarQube

Выполнил п. 1-4:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-04-hw.png)

Ошибки исправил - ошибок нет:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-05-hw.png)

Тут видно, что были ошибки, но сейчас их нет:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-06-hw.png)

В Issues также нет ошибок:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-07-hw.png)

## Знакомство с Nexus

### Основная часть

1. В репозиторий `maven-public` загрузите артефакт с GAV-параметрами:

 *    groupId: netology;
 *    artifactId: java;
 *    version: 8_282;
 *    classifier: distrib;
 *    type: tar.gz.
   
2. В него же загрузите такой же артефакт, но с version: 8_102.
3. Проверьте, что все файлы загрузились успешно.
4. В ответе пришлите файл `maven-metadata.xml` для этого артефекта.

## Решение - знакомство с Nexus

В репозиторий `maven-public` загрузил артефакт с GAV-параметрами:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-08-hw.png)

Репозиторий с загруженнымии артефактами разных версий:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-09-hw.png)

Файл `maven-metadata.xml` для артефекта: https://github.com/artmur1/19-03-cicd-hw/blob/main/files/maven-metadata.xml

### Знакомство с Maven

### Подготовка к выполнению

1. Скачайте дистрибутив с [maven](https://maven.apache.org/download.cgi).
2. Разархивируйте, сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
3. Удалите из `apache-maven-<version>/conf/settings.xml` упоминание о правиле, отвергающем HTTP- соединение — раздел mirrors —> id: my-repository-http-unblocker.
4. Проверьте `mvn --version`.
5. Заберите директорию [mvn](./mvn) с pom.

### Основная часть

1. Поменяйте в `pom.xml` блок с зависимостями под ваш артефакт из первого пункта задания для Nexus (java с версией 8_282).
2. Запустите команду `mvn package` в директории с `pom.xml`, ожидайте успешного окончания.
3. Проверьте директорию `~/.m2/repository/`, найдите ваш артефакт.
4. В ответе пришлите исправленный файл `pom.xml`.

## Решение - закомство с Maven

Удалил из `apache-maven-<version>/conf/settings.xml` упоминание о правиле, отвергающем HTTP- соединение:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-10-hw.png)

`mvn --version`:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-11-hw.png)

Поменяйте в `pom.xml` блок с зависимостями под свой артефакт:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-12-hw.png)

Запустил команду `mvn package` в директории с `pom.xml`, дождался успешного окончания:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-13-hw.png)

Проверил директорию `~/.m2/repository/`, нашел свой артефакт:

![alt text](https://github.com/artmur1/19-03-cicd-hw/blob/main/img/19-03-01-14-hw.png)

Исправленный файл `pom.xml`:

https://github.com/artmur1/19-03-cicd-hw/blob/main/files/pom.xml

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

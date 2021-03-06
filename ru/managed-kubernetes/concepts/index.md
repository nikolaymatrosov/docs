# Взаимосвязь ресурсов сервиса

[[!KEYREF k8s]](https://[!KEYREF k8s].io) — система для управления контейнерными приложениями. [!KEYREF k8s] предоставляет механизмы взаимодействия с кластером, с помощью которых осуществляется автоматизации развертывания, масштабирования и управления приложениями в контейнерах.

Основная сущность, которой оперирует сервис — _кластер [!KEYREF k8s]_. 

## Кластер [!KEYREF k8s] {#kubernetes-cluster} 

Кластер [!KEYREF k8s] состоит из мастера и одной или нескольких групп узлов. Мастер отвечает за управление кластером [!KEYREF k8s]. На узлах запускаются контейнеризованные приложения пользователя. 

Сервис полностью управляет мастером, а также следит за состоянием и работоспособностью группы узлов. Пользователь может управлять узлами напрямую, а также настраивать кластер [!KEYREF k8s] с помощью консоли управления Облака, CLI и API Managed Service for Kubernetes.

> [!IMPORTANT]
> 
> Группам узлов [!KEYREF k8s] требуется доступ в интернет для скачивания образов и компонентов.
> Предоставить доступ в интернет можно следующими способами: 
> - Назначить каждому узлу в группе [публичный IP адрес](../../vpc/concepts/address.md#publichnye-adresa).
> - [Настроить виртуальную машину в качестве NAT-шлюза](../operations/nat-instance.md). В таком случае будет использован только один публичный IP-адрес — тот, который присвоен шлюзу.

При работе с кластером [!KEYREF k8s] на инфраструктуре Яндекс.Облака задействуются следующие ресурсы:  

| Ресурс | Количество | Комментарий |
|----|:---:|----|
|Подсеть |2| [!KEYREF k8s] резервирует диапазоны IP-адресов, которые будут использоваться для подов и сервисов. |
|Таблица маршрутизации |1|Используется для маршрутизации трафика между подами внутри кластера Kubernetes.|
|Публичный IP |N|В количество N входит:</br> - **Один** публичный IP для NAT-шлюза.</br> - Публичный IP **каждому** узлу в группе, если вы используете технологию one-to-one NAT.</br> |

### Мастер {#master}

_Мастер_ — узел, который управляет кластером [!KEYREF k8s].

Мастер запускает управляющие процессы [!KEYREF k8s], которые включают сервер [!KEYREF k8s] API, планировщик и контроллеры основных ресурсов. Жизненный цикл мастера управляется сервисом при создании или удалении кластера [!KEYREF k8s]. Мастер отвечает за глобальные решения, которые выполняются на всех узлах кластера [!KEYREF k8s]. Они включают в себя планирование рабочих нагрузок, таких как контейнерные приложения, управление жизненным циклом рабочих нагрузок и масштабированием.

### Группа узлов {#node-group}

_Группа узлов_ — группа виртуальных машин с одинаковой конфигурацией в кластере [!KEYREF k8s], на которых запускаются пользовательские контейнеры. 

#### Конфигурация {#config} 

При создании группы узлов пользователь может сконфигурировать следующие параметры виртуальных машин:
- Тип виртуальной машины.
- Тип и количество ядер(vCPU).
- Объем памяти (RAM) и диска.

В одном кластере можно создавать группы с разными конфигурациями и размещать их в разных [зонах доступности](../../overview/concepts/geo-scope.md).

#### Подключение к узлам группы {#node-connect-ssh}

К узлам группы можно подключаться по SSH. О том, как это сделать, читайте в разделе [Подключиться к узлу по SSH](../operations/node-connect-ssh.md).

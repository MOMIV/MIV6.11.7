Задание 7. Автоматическое масштабирование приложения в Minikube с использованием HPA (Horizontal Pod Autoscaler)


Цель: Научиться настраивать автоматическое горизонтальное масштабирование (HPA) приложения в Minikube на основе метрик нагрузки, таких как использование процессора (CPU).


Описание задания:

* Запустите Minikube, если он еще не запущен.

* Для тестирования масштабирования разверните простое веб-приложение, например, Nginx.

* Установите Metrics Server.

* Создайте HPA для Nginx. Минимальное количество подов — 1. Максимальное — 5. --cpu-percent=50.

* Чтобы протестировать работу HPA, создайте нагрузку на приложение.

* Выполните команду, чтобы наблюдать за изменением количества подов в реальном времени.


В качестве решения необходимо сделать отчет, в котором видно, что количество подов увеличивается, исходя из нагрузки, а потом затухает, как только нагрузка закончилась.


Результат задания — после выполнения задания у вас будет развернутое в Minikube приложение, которое автоматически масштабируется в зависимости от нагрузки с помощью HPA.



Решение

1 Команда запуска Minikube

minikube start --extra-config=kubelet.housekeeping-interval=10s

2 Разворачиваем Nginx. Создаем HPA для Nginx. Минимальное количество подов — 1. Максимальное — 5. --cpu-percent=50

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/1.png)

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/2.png)

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/3.png)

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/6.png)


3 Установливаем Metrics Server

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/4.png)

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/5.png)

4 Чтобы протестировать работу HPA, создаем нагрузку на приложение

kubectl run -i --tty load-generator5 --image=busybox /bin/sh

while true; do wget -q -O- http://nginx-service:80; done

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/7.png)


5 Выполняем команду, чтобы наблюдать за изменением количества подов в реальном времени. Спустя время удаляем поды создающие нагрузку и наблюдаем умеьшение количества реплик.


![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/8.png)

![Image alt](https://github.com/MOMIV/MIV6.11.7/blob/main/screens/9.png)



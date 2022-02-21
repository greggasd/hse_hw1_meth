## Ссылка на google colab ноутбук

## Задание №1 - fastQC
### Общая статистика для ICM
![Снимок экрана 2022-02-21 в 05 48 47](https://user-images.githubusercontent.com/93208971/154883818-d5f48a1f-2545-48e0-91f5-720266a3fc02.png)

Полный отчет в репозиториий /reports
### Per sequence GC content
![Снимок экрана 2022-02-21 в 06 24 00](https://user-images.githubusercontent.com/93208971/154884065-3ed2c14e-bcb5-4745-889d-d33831941dae.png)

Фактические результаты сильно отклоняются о теоретических значений(синий график), у фактических значений GC наблюдается второй максимум в районе 70

## Задание №2
### a) Число ридов, закартированных на участки 11347700-11367700; 40185800-40195800.

![Снимок экрана 2022-02-21 в 06 33 11](https://user-images.githubusercontent.com/93208971/154884828-2ea9fdf7-c493-4cc7-849b-96c881b2a906.png)

 ### b) bash-скрипт для выполнения дедупликации для всех образцов одновременно и сводная таблица
 ```
 ! ls *pe.bam | xargs -P 4 -tI{} deduplicate_bismark  --bam  --paired  -o s_{} {}
 ```
 
 ![Снимок экрана 2022-02-21 в 06 35 33](https://user-images.githubusercontent.com/93208971/154885080-b1cd6423-7bf6-417e-b2a3-8648389378a0.png)
 
 ### c) и d) Коллинг метилирования цитозинов и скриншоты M-bias plot
 
 #### SRR3824222 - Epiblast
  ![Bismark M-bias Read 1](https://user-images.githubusercontent.com/93208971/154886168-ec6e3f5a-9280-461c-a3c7-5350b29b1a51.png)
  ![Bismark M-bias Read 2](https://user-images.githubusercontent.com/93208971/154886183-34d79100-d037-4468-a242-fc8ebcb53275.png)
 #### SRR5836473 - 8 cell
  ![Bismark M-bias Read 1 (1)](https://user-images.githubusercontent.com/93208971/154886364-6e8e1b91-d253-47d2-aa4b-581f57b495f8.png)
  ![Bismark M-bias Read 2 (1)](https://user-images.githubusercontent.com/93208971/154886377-04fcf516-9ef7-4fc2-bd2d-6b9d8b1e5dd2.png)
 #### SRR5836475 - ICM
  ![Bismark M-bias Read 1 (2)](https://user-images.githubusercontent.com/93208971/154886678-34366e19-6fb9-43c6-a80a-621b8f6dd740.png)
  ![Bismark M-bias Read 2 (2)](https://user-images.githubusercontent.com/93208971/154886683-03dc05d5-699a-454f-ba15-4d5a931146d6.png)
  
   ### e) Гистограммы распределения метилирования цитозинов по хромосоме
   
  #### Код на примере Epiblast, для остальных аналогично
  
  ```python
  
path = '/content/s_SRR3824222_1_bismark_bt2_pe.deduplicated.bedGraph'
bedGraph = pd.read_csv(path,  delimiter='\t', skiprows=1, header=None)
fig = plt.figure(figsize=(15, 5))
plt.title('Epiblast') 
plt.hist(bedGraph[3], bins=100, density=True)
plt.grid()
plt.xlabel('Процент')
plt.ylabel('Частота')
plt.show()
```
#### Epiblast
![Снимок экрана 2022-02-21 в 07 34 23](https://user-images.githubusercontent.com/93208971/154889821-788d68cb-4a6c-47e5-aacc-1203b1a4814d.png)
#### 8 cell
![Снимок экрана 2022-02-21 в 07 34 37](https://user-images.githubusercontent.com/93208971/154889822-28fa51f2-2f38-4edf-9c54-9e2b13ecf5f6.png)
#### ICM
![Снимок экрана 2022-02-21 в 07 34 56](https://user-images.githubusercontent.com/93208971/154889824-731f93e1-130b-4e49-845c-2ccfab686de2.png)




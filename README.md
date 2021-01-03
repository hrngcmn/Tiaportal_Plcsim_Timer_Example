# Tiaportal Plcsim Timer Example
Çalışma diyagramının açıklaması aşağıya eklenen örneğin düz zaman rölesi ve ters zaman rölesi kullanılarak ladder diyagramının oluşturulmasını içerir.
Simülasyonda çalıştıracağım için s7-1500 plc seçtim
tia portal ve plc sim programları versiyon16 dır. 

## Zamanlayıcının Çalışma Mantığı 
* Motor1 starta basıldığı anda çalışmaya başlayacaktır. 
* Motor1 çalıştıktan 7sn sonra motor2 çalışacaktır.
* Motor2 çalıştıktan 4sn sonra motor3 çalışacaktır. 
* Stop butonuna basılıncaya kadar 3 motor çalışmaya devam edecektir. 
* Stop butonuna basıldığından 6 sn sonra motor1 ve motor2 çalışmaya başlayacaktır. 
* motor1 ve motor2 çalışmaya başladıktan 5sn sonra duracaktır.

## Kullandığım PLC Tagları
![enter image description here](https://github.com/hrngcmn/Tiaportal_Plcsim_Timer_Example/blob/main/plctag.png?raw=true)

## Ladder Diyagramı ve açıklaması

### network 1
* stop butonu yardımcı rölenin enerjisini keser. 
* starta basıldıktan sonra sisteme elektriksel mühürleme atmıştır. bu sayede stopa basılıncaya kadar yardımcı röle1 çalışmaya devam edecektir. 
* Starta basılır basılmaz dzr1 7sn saymaya başlayacaktır. 
* 7sn sonunda motor2 çalışmaya başlayacaktır. ve dzr2 4sn saymaya başlayacaktır. 
* **Dikkat** Starta basılınca devreye giren ters zaman rölesi bulunmaktadır. Enerjilendiği anda kontakları konum değiştirir. Enerjisi kesildikten sonra saymaya başlar. Sayma işleminin sonunda kontakları ilk konumunu alır. 
![enter image description here](https://github.com/hrngcmn/Tiaportal_Plcsim_Timer_Example/blob/main/nw1.png?raw=true)

### network2
* Starta basılması ile yr bir aktif olur, açık kontağını kapatır. Motor1 çalışmaya balar. Dzr2 nin sayması bittiğinde durur. 
* paralel bağlanmış tzr1 sayesinde stopa basıldıktan sonra sayılan 6sn sonrasında motor1 tekrar çalışmaya başlar. 

![enter image description here](https://github.com/hrngcmn/Tiaportal_Plcsim_Timer_Example/blob/main/nw2.png?raw=true)

### network3
* Motor 3 ün çalışması dzr2 nin kontak kapatmasına bağlıdır. Kontak kapattıktan sonra dzr3 kontak açmasına kadar çalışmaya devam eder. 
* paralel bağlanmış tzr1 sayesinde stopa basıldıktan sonra sayılan 6sn sonrasında motor1 tekrar çalışmaya başlar. 
![enter image description here](https://github.com/hrngcmn/Tiaportal_Plcsim_Timer_Example/blob/main/nw3.png?raw=true)

## Simulasyon ekranı:
PlcSim programında simüle edilmiştir. 
![enter image description here](https://github.com/hrngcmn/Tiaportal_Plcsim_Timer_Example/blob/main/sim.png?raw=true)

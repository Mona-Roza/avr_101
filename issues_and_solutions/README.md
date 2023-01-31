## İçindekiler

* [Arduino As ISP](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#arduino-as-isp)

    * [Arduino'nun Programlayıcı Olarak Kullanılması](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#arduinonun-programlayıcı-olarak-kullanılması-sorunlar-ve-çözümler)

    * [Arduino ile Başka Bir Arduino'ya Bootloader Yüklenmesi](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#arduino-ile-başka-bir-arduinoya-bootloader-yüklenmesi)

    * [Arduino As ISP Yaşanabilecek Sorunlar ve Çözümleri](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#arduino-as-isp-yaşanabilecek-sorunlar-ve-çözümleri)

        * [avrdude: Device signature = 0xffffff](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#avrdude-device-signature--0xffffff)
        
        * [avrdude: Expected signature for ATMEGA328P is 1E 95 0F](https://github.com/Mona-Roza/Notes/tree/main/embedded_systems/issues_and_solutions#avrdude-expected-signature-for-atmega328p-is-1e-95-0f)

## Arduino As ISP:

Arduino'yu programlayıcı olarak kullanarak başka bir arduino kartınıza,

* bootloader olmadan programlama yapabilir, 

* bootloader yükleyebilir, 

* eski bootloader ile çalışıyorsa yeni bootloader'ı yükleyebilirsiniz.

Arduino'yu programlayıcı olarak kullanmak için aşağıdaki adımları takip edin:

:warning: Burada Arduino Uno kartı programlayıcı olarak kullanılırken başka bir Arduino Uno kartı ise hedef kart olarak kullanılmıştır. Ancak programcı karttan hedef karta giden bağlantıları aynı şekilde kurarak farklı model kartlarda da aynı yol izlenerek işlemler gerçekleştirilebilir.

### Arduino'nun Programlayıcı Olarak Kullanılması:
Bu yöntemde hedef kart içerisindeki bootloader komple yokedilir. Bu yöntemi kullandıktan sonra hedef kartın tekrar bilgisayar aracılığıyla kullanılabilmesi için bir kart yardımıyla içerisine bootloader yüklenmesi gerekir. 

1. Programlayıcı kartı bilgisayarınıza takın ve Arduino IDE'yi açın. 

2. Arduino IDE içerisinde "Dosya" seçeneğinin altında bulunan "Örnekler" sekmesinden 11.ArduinoISP örneğini açın.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/1.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/1.png)

3. Bu örneği, derledikten sonra programlayıcı olarak kullanacağınız Arduino kartına yükleyin. 

4. Aşağıdaki devre şemasını gerçekleyin. (Hedef kart farklı olsa da girişler bu şekilde olmalıdır. Programcının 13,12,11, GND pinleri, hedefin aynı isimli pinlerine, programcının 10 numaralı pini hedefin Reset pinine, programcının 5V pini hedefin Vcc veya Vin pinine bağlanmalıdır.)

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/2.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/2.png)

5. Programcı kartı bilgisayarınıza bağlayarak yeni bir Arduino IDE sayfası açın.

6. Aşağıdaki kodu Arduino IDE'ye yapıştırın.

```
void setup() {
    pinMode(7, OUTPUT);
    pinMode(6, OUTPUT);
}

void loop() {
    digitalWrite(7, HIGH);
    digitalWrite(6, LOW);
    delay(200);
    digitalWrite(6, HIGH);
    digitalWrite(7, LOW);
    delay(200);
}
```

7. Hedef kartın modelini ve programlayıcı kartı bağladığınız portu seçin.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/3.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/3.png)

8. "Araçlar" menüsünden "Programlayıcı" seçeneğinin altından "Arduino As ISP" seçeneğini seçin.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/4.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/4.png)

9. "Eskiz" menüsünün altından "Programlayıcı Kullanarak Yükle" seçeneğini seçerek kodu programlayıcı kart aracılığıyla diğer karta yükleyin.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/5.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/5.png)

### Arduino ile Başka Bir Arduino'ya Bootloader Yüklenmesi:

1. Programlayıcı kartı bilgisayarınıza takın ve Arduino IDE'yi açın. 

2. Arduino IDE içerisinde "Dosya" seçeneğinin altında bulunan "Örnekler" sekmesinden 11.ArduinoISP örneğini açın.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/1.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/1.png)

3. Bu örneği, derledikten sonra programlayıcı olarak kullanacağınız Arduino kartına yükleyin. 

4. Aşağıdaki devre şemasını gerçekleyin. (Hedef kart farklı olsa da girişler bu şekilde olmalıdır. Programcının 13,12,11, GND pinleri, hedefin aynı isimli pinlerine, programcının 10 numaralı pini hedefin Reset pinine, programcının 5V pini hedefin Vcc veya Vin pinine bağlanmalıdır.)

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/2.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/2.png)

5. Programcı kartı bilgisayarınıza bağlayarak yeni bir Arduino IDE sayfası açın.

6. Hedef kartın modelini ve programlayıcı kartı bağladığınız portu seçin.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/3.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/3.png)

7. "Araçlar" menüsünden "Programlayıcı" seçeneğinin altından "Arduino As ISP" seçeneğini seçin.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/4.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/4.png)

8. "Araçlar" menüsünden "Bootloader'ı Yükle" seçeneğini seçin. Böylelikle hedef kartınıza bootloader'ı yüklemiş olacaksınız.

[![](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/6.png)](https://github.com/Mona-Roza/Notes/blob/main/embedded_systems/issues_and_solutions/images/6.png)

### Arduino As ISP Yaşanabilecek Sorunlar ve Çözümleri:

#### avrdude: Device signature = 0xffffff 

"Device signature = 0xffffff" hatasını alırsanız muhtemelen kablo bağlantılarında bir hata yapmışsınızdır. Kablo bağlantılarının doğru olduğuna emin olduktan sonra tekrar deneyin.

#### avrdude: Expected signature for ATMEGA328P is 1E 95 0F

"Expected signature for ATMEGA328P is 1E 95 0F" veya "Yikes!  Invalid device signature." Hatalarından bir tanesini alırsanız, hedef kartınızın Mikrocontroller'i büyük ihtimalle ATMEGA328P değil **ATMEGA328PB**'dir. Bu sorunu çözmek için,aşağıdaki adımları takip edin:

1. Windows'ta (USER_NAME kısmını kendi bilgisayar isminize göre düzenlemelisiniz) `C:\Users\USER_NAME\AppData\Local\Arduino15\packages\arduino\tools\avrdude\6.3.0-arduino17\etc` konumuna, MacOS'ta ise (USER_NAME kısmını kendi bilgisayar isminize göre düzenlemelisiniz) `Users/USER_NAME/Library/Arduino15/packages/arduino/tools/avrdude/6.3.0-arduino17/etc` konumuna gidin ve **avrdude.conf** dosyasının öncelikle herhangi bir konuma **yedeğini alın** ardından dosyayı açın.

2. Windows için `CTRL + F`, MacOS için `Command  + F` kısayollarını kullanarak dosyada `m328` kelimesini aratın.

3. `m328` kelimesini arattığınızda bu kelimenin geçtiği bir çok yer olacaktır, endişelenmeyin, bizim aradığımız bunlardan ikincisi yani ilerleyen satırları şu şekilde olan:

```
...

part parent "m328"
    id			= "m328p";
    desc		= "ATmega328P";
    signature		= 0x1e 0x95 0x0F;

    ocdrev              = 1;
;
...
```

4. `signature		= 0x1e 0x95 0x0F;` kısmını `signature		= 0x1e 0x95 0x16;` ile değiştirip dosyayı kaydedin.

5. Arduino IDE'nizi tekrar başlatıp programlayıcı kullanarak programlamak istediğiniz kartı, tekrar programlama işlemini yapın.

:warning: Programcı kullanarak programlama yapmaya devam etmeyecekseniz, yedeklediğiniz config dosyasını tekrar aynı konumlara atın ve normal şekilde programlamaya devam edin. Eğer config dosyasını eski haline getirmezseniz, normal bir biçimde programlama yapamayabilirsiniz.

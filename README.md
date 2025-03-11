# Serverda-Nasil-Eklenti-Calistiririm

Dostlar malum DePin hype ile beraber birçok projenin uzantılarını tarayıcımıza ekleyip çalıştırıyoruz. Bunun PC'nin sürekli açık kalmak ve arka planda CPU kullanmaya devam etmek gibi olumsuz çıktıları var. Bunu aşabilmek için bir sunucu kiralayıp Chromium kuracağız ve eklentileri tek tek tarayıcımıza ekleyip PC'den bağımsız puan toplamaya ve kazancımızı artırmaya çalışacağız.


Öncelikle bir sunucu kiralamak gerekiyor. Ben Hetzner firmasından 3 Euro'luk en ucuz sunucuyu kiraladım. Eğer Hetzner üyeliğiniz yoksa size 20€ kredi veren [buradan](https://hetzner.cloud/?ref=RacCSRmrsndd) üye olabilirsiniz. Sunucunuz hazırsa kuruluma geçebiliriz.

## Docker Kurulumu

```
sudo apt update -y && sudo apt upgrade -y
```
```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```
sudo apt-get update
```
```
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
sudo apt update -y && sudo apt upgrade -y
```
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Versiyon Kontrolü

Çıktı "27.5.1, build 9f9e405" şeklindeyse devam
```
docker --version
```

## Chromium Kurulumu

```
mkdir chromium
```

### Chromium dizinine gidelim

```
cd chromium
```

## Docker Compose Dosyası Yapılandırma

```
nano docker-compose.yaml
```

Aşağıdaki kodu tek seferde kopyalayıp yapıştıralım. Sonra klavyeden CTRL+X yapıp Y tıklayalım ve en son ENTER tıklayıp kaydedip çıkalım

```
---
services:
  chromium:
    image: lscr.io/linuxserver/chromium:latest
    container_name: chromium
    security_opt:
      - seccomp:unconfined #optional
    environment:
      - CUSTOM_USER=     #Replace username
      - PASSWORD=    #Replace password
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - CHROME_CLI=https://x.com/cryptograsi #optional
    volumes:
      - /root/chromium/config:/config
    ports:
      - 3010:3000   #Change 3010 to your favorite port if needed
      - 3011:3001   #Change 3011 to your favorite port if needed
    shm_size: "1gb"
    restart: unless-stopped
```

## Chromium Çalıştırma

```
docker compose up -d
```

Şimdi tarayıcımıza geçip aşağıdaki adreslerden birini kullanarak sunucumuza direkt bağlanıp tarayıcımıza eklentilerimizi ekleyebiliriz.

```
http://SunucunuzunIPsi:3010/
https://SunucunuzunIPsi:3011/
```


Ben altta sıraladığım eklentileri çalıştırıyorum. Eğer sizin hala çalıştırmadığınız varsa siz de tarayıcınıza ekleyip PC'nizi yormadan para kazanmaya başlayabilirsiniz

#### 1) Voltiz.AI:



[Buradan](https://voltix.ai/dashboard/salenodes?ref=F6IRN) kayıt olun ve uzantısını indirip çalıştırın. PC’nizin durumuna göre “easy, normal ya da hard” seçip puan kazanmaya başlayabilirsiniz.



#### 2) MeshChain:



[Buradan](https://app.meshchain.ai?ref=OLC6I2MQA74V) kayıt olup uzantısını çalıştırın. Her 3 saatte puanları claim etmek gerekiyor. Bunda ayrıca telegram nodu da mevcut. Dilerseniz onu da 3 saatte bir aktifleyebilirsiniz.



#### 3) Stork Oracle:
4.5 Milyon dolar yatırım aldı.
[Buradan](https://chromewebstore.google.com/detail/stork-verify/knnliglhgkmlblppdejchidfihjnockl) eklentiyi kurun ve M5DGVQTLAQ kodunu kayıt olurken girin



#### 4) Kaisar:
[Buradan](https://zero.kaisar.io/register?ref=ojclWt827) kayıt olup sol alt taraftaki “Download Extension” yazan yere tıklayıp uzantısını çalıştırın. Günlük check-in yapın.



#### 5) LayerEdge.io:
[Buradan](https://dashboard.layeredge.io/) kayıt olun ve kod sorduğunda “ eLJI3dxN “ kodunu girin. Yakında CLI nodu da gelecek.



#### 6) Functor Network:
[Buradan](https://node.securitylabs.xyz/?from=extension&type=signin&referralCode=cm3aknd6zc4xgmt1bj8bsxama) kayıt olduktan sonra 24 saatte bir check işlemi var. Size dahil olabilmeniz için kod soracaktır, o kısma “cm3aknd6zc4xgmt1bj8bsxama” kodunu yapıştırıp devam edin, eklentisini çalıştırın ve burner cüzdan ile işlemleri yapın.



#### 7) NodeGo:
8M dolar yatırım almış bir proje.
[Buradan](https://app.nodego.ai/r/NODEA7CBFC26308E) kayıt olalım, kod sorarsa “NODEA7CBFC26308E” girin. Dashboard’da sol alttaki “Dekstop Node” ve “Telegram Node” yazan yerlere tıklayarak her iki nodu da çalıştırabilirsiniz.



#### 8) Primus Labs:
6.5M dolar yatırım aldı.
Eklentiyi  [buradan](https://chromewebstore.google.com/detail/primus-prev-pado/oeiomhmbaapihbilkfkhmlajkeegnjhe) kurun.
Sizden kod isteyecek, “257PAOL” kodunu girin ekstra puan verecek. 



#### 9) Blockcast:
Henüz uzantısı yok,  [buradan](http://10.0.2.112:3000?referral-code=tK6Qzf) kayıt olup sosyal medya görevlerini tamamlayalım ve erkenden yerimizi alalım.



#### 10) Teneo:
[Buradan](https://chromewebstore.google.com/detail/teneo-community-node/emcclcoaglgcpoognfiggmhnhgabppkm) eklentiyi kurun ve kayıt olurken “bh2nK” kodunu girip ekstra puan kazanın.



#### 11) Aigaea: 
[Buradan](https://app.aigaea.net/register?ref=gasrYgeZzxX362) girip kayıt olun. Biraz kurcalayın, sosyal görevler ve anket doldurarak bir profil mintleme işi var. Bunları tamamlamaya çalışın.



#### 12) Toggle:
[Buradan](https://toggle.pro/sign-up/69e0bffa-b45f-4b55-957f-477dc32a7f56) register yapıp eklentiyi tarayıcınıza kurun. Ara sıra kontrol etmek gerekiyor çünkü bazen bağlantısı kopuyor. Yeniden bağlanmak için eklentiden “connect” butonuna basmak gerek.



#### 13) DeSpeed:
[Buradan](https://app.despeed.net/register?ref=eWeZvpjmjTVO) kayıt olup uzantısını çalıştırın. Günlük check-in yapıp sosyal görevleri tamamlayın.



#### 14) Bless Network:
[Buradan](https://bless.network/dashboard?ref=H63JOD) kayıt olup X ve DC görevlerini tamamlayın.



#### 15) Dawn:
[Buradan](https://chromewebstore.google.com/detail/dawn-validator-chrome-ext/fpdkjdnhkakefebpekbdhillbhonfjjp) uzantıyı kurun ve kayıt olurken ekstra puan kazanmak için “bxy3bigj” kodunu girin.



#### 16) Naoris:
11.5M dolar yatırım aldı, önemli bir proje.
[Buradan](https://chromewebstore.google.com/detail/naoris-protocol-browser-s/cpikalnagknmlfhnilhfelifgbollmmp) eklentisini kurun ve kayıt olurken “mZiQ6JFPDd1HAdHb” kodunu girin, kodsuz kayıt olmak mümkün değil.



#### 17) Blockmesh:
[Buradan](https://app.blockmesh.xyz/register?invite_code=d75fa421-9185-4c79-8c70-ab053e0734cc) kayıt olduktan sonra eklentisini kurun ve “Perks” sayfasını açarak görevleri tamamlayın.



#### 18) Gaianet:
Son demlerini yaşıyor olabiliriz ama en azından sosyal medya görevlerini tamamlayıp yerinizi almak isterseniz [buradan](https://gaianet.ai/reward?invite_code=Rr1PJc) kayıt olabilirsiniz: 
Gaianet’in CLI nodu da mevcut. Eğer hızlıca puan kazanmak isterseniz [benimle](https://x.com/cryptograsi) X üzerinden dm ile iletişime geçebilirsiniz.



#### 19) Oasis:
[Buradan](https://r.distribute.ai/2417ad21581df515) kayıt olup eklentiyi pc’ye indiriyoruz. Bu nod tarayıcıya eklenmiyor, pc’de çalıştırıyoruz.



#### 20) Grass:
Uzun zamandır çalıştırdığım bir eklenti, DePin eklentilerinin öncüsü diyebiliriz. Tokeni markette listeli. Çok ödül vereceğini sanmam fakat çalıştırmak isterseniz [buradan](https://app.getgrass.io/register/?referralCode=sPgtuWYvWZKv7UC) kayıt olabilirsiniz: 



#### 21) NodePay:
Tokeni listeli ve yine çok ödül vermesi düşük olan bir proje. Bunu da Grass gibi kenarda dursun diyerek çalıştırmak isterseniz [buradan](https://app.nodepay.ai/register?ref=aSetmleGqAzVRWt) kayıt olun



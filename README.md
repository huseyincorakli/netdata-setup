# Netdata Kurulum ve Güvenlik Konfigürasyonu

## 1. Netdata Kurulumu

Netdata'yı sunucuya kurmak için tek komut:
```bash
wget -O /tmp/netdata-kickstart.sh https://my-netdata.io/kickstart.sh && sh /tmp/netdata-kickstart.sh
```


## 2. Güvenlik Ayarları

Netdata varsayılan olarak 19999 portunda çalışır ve herkese açıktır. Güvenlik için şu adımları uyguladık:

### 2.1 IP Erişim Kısıtlaması

1. Konfigürasyon dosyasını düzenleme:
```bash
sudo nano /etc/netdata/netdata.conf
```

2. Web erişim ayarları:
```conf
[web]
    bind to = *:19999
    allow connections from = localhost ip_adresiniz
```
Bu ayarlar:
- `bind to = *:19999`: Tüm network arayüzlerinde 19999 portunu dinle
- `allow connections from`: Sadece localhost ve belirtilen IP adresinden erişime izin ver

### 3.1 Servis Yeniden Başlatma
```bash
sudo systemctl restart netdata
```

### 3.2 Servis Durumu Kontrolü
```bash
sudo systemctl status netdata
```

## 4. Kontrol ve Test

- Firewall durumu kontrol:
```bash
sudo ufw status
```

- netdata kontrolü:
```bash
sudo systemctl status netdata
````

## 5. Önemli Notlar

- Netdata varsayılan port: 19999
- Konfigürasyon dosyası konumu: `/etc/netdata/netdata.conf`
- Sadece izin verilen IP adreslerinden erişim sağlanabilir
- Servis değişikliklerinden sonra mutlaka yeniden başlatılmalı


## 6. Hata Giderme

Eğer "Connection refused" hatası alırsanız:
1. Servis durumunu kontrol edin
2. IP adresinin doğru olduğundan emin olun
3. Konfigürasyon dosyasını kontrol edin
4. Servisi yeniden başlatın
5. Logları kontrol edin

# Docker-Laravel-OpenAdmin Kurulumu

## Adım 1: Repoyu Klonlayın
İlk olarak, projeyi klonlayın:  
```bash
git clone https://github.com/alperenbugaz/laravel-docker-openadmin.git
```
## Adım 2: Docker Servislerini Başlatın

Docker servislerini başlatmak için aşağıdaki komutu kullanın:

```bash
docker compose up -d
```
## Adım 3: Laravel'i Kurun
PHP konteynerini açın ve Laravel'i kök dizininde kurun:

```bash
composer create-project laravel/laravel .
```


## Adım 4: Yazma İzinlerini Ayarlayın
Eğer yazma izinleri ile ilgili sorun yaşarsanız, PHP konteyneri terminalinde aşağıdaki komutları çalıştırarak gerekli izinleri verin:
```bash
chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
chmod -R 775 /var/www/html/storage /var/www/html/bootstrap/cache
```
komutlarını çalıştırarak yazma izinlerini verin.
## Adım 5: .env Dosyasını Yapılandırın
Kurulumun yapıldığı dizinde bulunan .env dosyasını açın ve veritabanı bağlantı ayarlarını aşağıdaki şekilde yapılandırın:
```bash
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel-docker
DB_USERNAME=root
DB_PASSWORD=root
```
## Adım 6: Veritabanı Tablolarını Oluşturun
Veritabanı tablolarını oluşturmak için aşağıdaki komutu çalıştırın:


```bash
php artisan migrate
```

## Adım 7: Uygulamanızı Kontrol Edin

[http://localhost:8012](http://localhost:8012) adresine giderek laravelin kurulduğuna ve [http://localhost:8080/](http://localhost:8080/) (kullanıcı adı: admin, şifre: root) adresine girerek tabloların oluştuğuna emin olun. 
## Adım 8: Open-Admin Paketini Kurun
Open-Admin paketini kurmak için aşağıdaki adımları izleyin:

 1.  composer require komutunu çalıştırarak Open-Admin paketini yükleyin:
```bash
composer require open-admin-org/open-admin:* --with-all-dependencies
```
2. Paket konfigürasyon dosyalarını yayınlamak için:
```bash
php artisan vendor:publish --provider="OpenAdmin\Admin\AdminServiceProvider"
```
3. Open-Admin'ı kurmak için:
```bash
php artisan admin:install
```
## Adım 9: Open-Admin Kurulumunu Tamamlandı
Kurulum işlemi tamamlandıktan sonra, [http://localhost:8012/admin](http://localhost:8012/admin) adresine giderek login panelini görebilirsiniz.

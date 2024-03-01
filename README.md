# EFK Stack Docker Compose Kurulumu

Bu repo, log yönetimi ve analizi için kullanılan EFK (Elasticsearch, Fluentd, Kibana) stack'ının Docker Compose ile kurulumunu içermektedir. EFK stack'ı, çeşitli kaynaklardan logları toplamanıza, Elasticsearch'te saklamanıza ve Kibana üzerinden görselleştirmenize olanak tanır.

## Bileşenler

- __Elasticsearch__: Yüksek ölçeklilik ve gerçek zamanlı arama yetenekleri sunan, RESTful API üzerinden erişilebilen bir arama ve analiz motorudur.
- __Fluentd__: Çeşitli kaynaklardan log ve veri akışlarını toplayıp, işleyip, farklı hedeflere yönlendirerek veri entegrasyonunu kolaylaştıran açık kaynak bir veri kolektörüdür.
- __Kibana__: Elasticsearch'te saklanan verileri sorgulamak, görselleştirmek ve analiz etmek için kullanılan, web tabanlı bir görselleştirme aracıdır.

## Gereksinimler

- Docker
- Docker Compose

## Kurulum Talimatları

### **Reposu klonlayın**
```bash
  git clone https://github.com/mustafadikyar/fluentd-elasticsearch-kibana.git
  cd fluentd-elasticsearch-kibana
```
### Stack'ı Oluşturun ve Çalıştırın

Docker Compose kullanarak `docker-compose.yml` dosyasında tanımlanan servisleri oluşturun ve çalıştırın:

```bash
  docker-compose up --build -d
```

Bu komut, tüm servisleri arka planda başlatır.

### Servislere Erişim

- **Kibana**: Kibana arayüzüne erişmek için web tarayıcınızda [http://localhost:5601](http://localhost:5601) adresini açın.
- **Elasticsearch**: [http://localhost:9200](http://localhost:9200) adresinde erişilebilir.
- **Fluentd**: TCP ve UDP port `24224` üzerinden ve HTTP port `8888` üzerinden logları kabul eder.

### Fluentd Konfigürasyonu

Fluentd servisi, TCP/UDP port `24224` ve HTTP port `8888` üzerinden gönderilen logları toplamak için yapılandırılmıştır. Loglar işlendikten sonra Elasticsearch'e yönlendirilir ve burada saklanır. Daha sonra Kibana kullanılarak loglar görselleştirilebilir ve analiz edilebilir.

### Fluentd'ye Log Gönderme

Fluentd'ye log göndermek için çeşitli input plugin'leri kullanılabilir. Örneğin, HTTP üzerinden log göndermek için aşağıdaki `curl` komutunu kullanabilirsiniz:

```bash
  curl -X POST -d 'json={"action":"login","user":2}' http://localhost:8888/<tag>
```


`<tag>`'i log verileriniz için uygun bir etiketle değiştirin.

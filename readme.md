# Tugas 5 Big Data - Spark with Docker
Tugas 5 ini, saya mencoba menjalankan Spark with Docker, dengan beberapa spesifikasi berikut:
- spesifikasi 1
    Jumlah worker: 2
    Jumlah CPU: 2, dengan 1 core tiap worker
    Memory: 1G
    Partisi: 100 dan 1000
- spesifikasi 2
    Jumlah worker: 2
    Jumlah CPU: 4, dengan 2 core tiap worker
    Memory: 1G
    Partisi: 100 dan 1000
- spesifikasi 3
    Jumlah worker: 5
    Jumlah CPU: 2, dengan 1 core di 2 worker
    Memory: 1G
    Partisi: 100 dan 1000
- spesifikasi 4
    Jumlah worker: 5
    Jumlah CPU: 4, dengan 1 core di 4 worker
    Memory: 1G
    Partisi: 100 dan 1000

File yang digunakan untuk mengetes spesifikasi tersebut adalah file pi.py, file untuk menghitung nilai pi, dimana telah disediakan oleh Apache Spark (examples/src/main/python/pi.py).

Berikut adalah hasil dari test tersebut:

## 1. Spesifikasi 1
Konfigurasi dari docker-compose.yml adalah sebagai berikut:
```
version: '2'

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```

![](/screenshot/1.1.png)

![](/screenshot/1.2.png)

Hasil dari test adalah sebagai berikut:
- 100 partisi
![](/screenshot/1.5.1.png)
![](/screenshot/1.6.1.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.148160, dengan waktu 40s

- 1000 partisi
![](/screenshot/1.5.2.png)
![](/screenshot/1.6.2.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.146740, dengan waktu 2.0 min


## 2. Spesifikasi 2
Konfigurasi dari docker-compose.yml adalah sebagai berikut:
```
version: '2'

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=2
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=2
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```

![](/screenshot/2.1.png)

![](/screenshot/2.2.png)

Hasil dari test adalah sebagai berikut:
- 100 partisi
![](/screenshot/2.5.1.png)
![](/screenshot/2.6.1.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.137101, dengan waktu 1.1 min

- 1000 partisi
![](/screenshot/2.5.2.png)
![](/screenshot/2.6.2.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.133723, dengan waktu 1.9 min

## 3. Spesifikasi 3
Konfigurasi dari docker-compose.yml adalah sebagai berikut:
```
version: '2'

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-3:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=0
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-4:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=0
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-5:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=0
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```

![](/screenshot/3.1.png)

![](/screenshot/3.2.png)

Hasil dari test adalah sebagai berikut:
- 100 partisi
![](/screenshot/3.5.1.png)
![](/screenshot/3.6.1.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.141527, dengan waktu 1.9 min

- 1000 partisi
![](/screenshot/3.5.2.png)
![](/screenshot/3.6.2.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.147340, dengan waktu 2.3 min

## 4. Spesifikasi 4
Konfigurasi dari docker-compose.yml adalah sebagai berikut:
```
version: '2'

services:
  spark:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=master
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
    ports:
      - '8080:8080'
  spark-worker-1:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-2:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-3:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-4:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=1
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
  spark-worker-5:
    image: bitnami/spark:2
    environment:
      - SPARK_MODE=worker
      - SPARK_MASTER_URL=spark://spark:7077
      - SPARK_WORKER_MEMORY=1G
      - SPARK_WORKER_CORES=0
      - SPARK_RPC_AUTHENTICATION_ENABLED=no
      - SPARK_RPC_ENCRYPTION_ENABLED=no
      - SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no
      - SPARK_SSL_ENABLED=no
```

![](/screenshot/4.1.png)

![](/screenshot/4.2.png)

Hasil dari test adalah sebagai berikut:
- 100 partisi
![](/screenshot/4.5.1.png)
![](/screenshot/4.6.1.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.138341, dengan waktu 3.3 min

- 1000 partisi
![](/screenshot/4.5.2.png)
![](/screenshot/4.6.2.png)

Dari gambar diatas, kita dapat mengetahui bahwa hasil pi-nya adalah 3.139542, dengan waktu 7.5 min


## Kesimpulan

Beberapa kesimpulan yang saya dapat:
1. Penambahan partisi dari sebuah spesifikasi akan menambah waktu proses penyelesaiannya.
2. Penambahan core akan membuat waktu proses lebih cepat selesai dan hasil lebih akurat karena mendekati hasil benar.
3. Penambahan worker akan membuat waktu proses lebih lama, namun hasil lebih akurat.

Terima kasih.
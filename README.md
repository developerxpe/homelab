# homelab / stacks

Bu depo, Colima (Docker) üzerinde çalışan homelab servislerini tek bir
`docker-compose.yml` ile yönetir. Sırlar (`.env`, sertifikalar, veritabanları)
repoda **tutulmaz**; çalışma anında yerelde kalır.

## Stack'ler

| Klasör / dosya | Ne işe yarar | Repoda tutulan | Yerelde / secret (gitignore) |
|---|---|---|---|
| `docker-compose.yml` | Tüm servislerin tanımı | servisler + healthcheck | — |
| `.env.example` | Ortam değişkenleri örneği | şablon (değersiz) | `.env` (gerçek değerler) |
| `glance/` | Glance dashboard | `glance.yml` | — |
| `npm/` | Nginx Proxy Manager | `data/nginx/proxy_host/*.conf` | `data/database.sqlite`, `letsencrypt/` |
| `cloudflared/` | Cloudflare tunnel | `config.yml` | `cert.pem`, `<uuid>.json` |
| `vaultwarden/` | Vaultwarden | — | `vw-data/` |
| `beszel_data/` | Beszel hub verisi | — | tüm içerik |
| `beszel_socket/` | Beszel unix socket | — | tüm içerik |
| `beszel_agent_data/` | Beszel agent durumu | — | tüm içerik |
| `pma/` | phpMyAdmin `/config` | — | tüm içerik |
| `foto/` | foto uygulaması imajı | `Dockerfile` | — |
| `coolify/` | Coolify (ayrı kurulum) | — | tüm içerik |
| `twingate/` | Twingate connector | `docker-compose.yml` | `.env` |
| `9router/` | 9router uygulaması | kaynak dosyalar | — |

## Kurulum

```sh
cp .env.example .env   # değerleri doldur
docker compose up -d
```

## Notlar

- Sırlar asla commit edilmez (`.gitignore`).
- Veri klasörleri (`beszel_*`, `vaultwarden`, `pma`, `coolify`) repoda sadece
  `.gitkeep` ile görünür; gerçek veriler yerelde kalır.
- MySQL verisi harici named volume `mysql-data-ehrns7aim82b88ib31psbkfw`
  içindedir; `docker compose down -v` **çalıştırılmamalı**.

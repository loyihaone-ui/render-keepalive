# render-keepalive

LeadersAcademy sayti uchun Render **free tier** keep-alive.

Render bepul tarif 15 daqiqa harakatsizlikdan keyin serverni uxlatadi.
Keyingi birinchi so'rov 30–60 soniya kutadi. Bu repo GitHub Actions orqali
har **12 daqiqada** `/health` ga ping yuborib, serverni uyg'oq tutadi.

## Qanday ishlaydi

| Qism | Vazifasi |
|---|---|
| `ping` job | `https://leadersacademy.onrender.com/health` ga so'rov; 5 martagacha qayta urinish |
| `heartbeat` job | oyiga bir marta `alive.txt` ni yangilaydi — GitHub 60 kun harakatsizlikdan keyin jadvalni o'chirmasligi uchun |

Cron: `*/12 * * * *` (UTC), ya'ni kechayu kunduz har 12 daqiqada.

> Nega alohida repo: GitHub Actions private repo uchun oyiga 2000 daqiqa beradi,
> 24/7 `*/12` esa ~3600 daqiqa talab qiladi. Public repo'da daqiqalar cheksiz,
> shuning uchun asosiy loyiha kodi private qoladi.

## Qo'lda tekshirish

Repo → **Actions** → *Render keep-alive* → **Run workflow**.

Yoki to'g'ridan-to'g'ri:

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://leadersacademy.onrender.com/health
```

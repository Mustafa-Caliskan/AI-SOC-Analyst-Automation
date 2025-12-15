# 🛡️ AI-Powered SOC Analyst Automation

Bu proje, **Splunk SIEM**'den gelen güvenlik alarmlarını **Yapay Zeka (Llama 3 / Gemini)** ve **Tehdit İstihbaratı (VirusTotal)** servislerini kullanarak otomatik analiz eden ve raporlayan bir **n8n** otomasyonudur.

![Workflow Görünümü](workflow.png)

## 🚀 Projenin Amacı
Geleneksel SOC süreçlerinde analistler binlerce logu manuel inceler. Bu otomasyon şunları yapar:
1.  **Splunk**'tan gelen alarmları (Webhook) yakalar.
2.  Şüpheli IP adresini **VirusTotal** API ile tarar.
3.  **Groq (Llama 3)** yapay zekasını kullanarak saldırı tipini (SQL Injection, Brute Force vb.) analiz eder.
4.  Log zamanını otomatik olarak **Yerel Saate (TR)** çevirir.
5.  Analiste **aksiyon alınabilir, profesyonel formatta** bir e-posta raporu gönderir.

## 📊 Örnek Rapor Çıktısı

Sistem, analiste aşağıdaki formatta otomatik bir rapor üretir:

![Rapor Örneği](report-sample.png)

## 🛠️ Kurulum ve Kullanım

1.  Bu repodaki `.json` dosyasını indirin.
2.  n8n panelinizde "Import Workflow" diyerek dosyayı yükleyin.
3.  Düğümlerin içine kendi **Webhook**, **VirusTotal** ve **LLM** API anahtarlarınızı girin.
4.  Workflow'u aktifleştirin.

---
*Bu proje siber güvenlik operasyonlarını otomatize etmek amacıyla geliştirilmiştir.*

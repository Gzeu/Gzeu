# 🎯 GitHub Sponsors Monitoring System

> Sistemul automat de monitorizare și notificare pentru GitHub Sponsors, 100% gratuit cu GitHub Actions.

## 🚀 Funcționalități

- ✅ **Monitorizare automată** - Verifică sponsorii la fiecare 6 ore
- 🔔 **Notificări multiple** - Discord, Email, Telegram
- 📊 **Statistici** - Urmărește numărul de sponsori și venitul lunar
- 🔐 **Acces automat** - Acordă acces la repo-uri private pentru sponsori
- 💾 **Istoric complet** - Păstrează istoric cu toți sponsorii
- 🎨 **Notificări frumoase** - Template-uri profesionale pentru toate platformele

## ⚙️ Configurare Rapidă

### 1. Configurare Secrete GitHub

Mergi la **Settings** > **Secrets and variables** > **Actions** în repo-ul `Gzeu/Gzeu` și adaugă:

#### 🔑 Secrete Obligatorii:
```bash
# Pentru acces la API-ul GitHub Sponsors
GH_PAT = "ghp_your_personal_access_token_here"
```

#### 📱 Secrete pentru Notificări (opționale):

**Discord:**
```bash
DISCORD_WEBHOOK = "https://discord.com/api/webhooks/your_webhook_url"
```

**Email (Gmail SMTP):**
```bash
SMTP_USERNAME = "your-email@gmail.com"
SMTP_PASSWORD = "your-app-password"
NOTIFICATION_EMAIL = "recipient@gmail.com"
```

**Telegram:**
```bash
TELEGRAM_BOT_TOKEN = "your_bot_token_from_botfather"
TELEGRAM_CHAT_ID = "your_chat_id"
```

---

## 📋 Ghid Pas cu Pas

### 🔐 Pas 1: Creează Personal Access Token (PAT)

1. Mergi la [GitHub Settings > Developer settings > Personal access tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Selectează scope-urile:
   - ✅ `read:user`
   - ✅ `read:org`
   - ✅ `repo` (pentru acces la repo-uri private)
4. Copiază token-ul și adaugă-l ca `GH_PAT` în secrete

### 🎮 Pas 2: Discord Webhook (Opțional)

1. Pe serverul Discord, mergi la **Server Settings** > **Integrations**
2. Click **Create Webhook**
3. Configurează webhook-ul:
   - **Name**: `Sponsor Bot`
   - **Channel**: alege channel-ul pentru notificări
4. Copiază **Webhook URL** și adaugă-l ca `DISCORD_WEBHOOK`

### 📧 Pas 3: Email Notifications (Opțional)

**Pentru Gmail:**
1. Activează [2-Factor Authentication](https://myaccount.google.com/security)
2. Generează [App Password](https://myaccount.google.com/apppasswords)
3. Adaugă secretele:
   - `SMTP_USERNAME`: adresa ta Gmail
   - `SMTP_PASSWORD`: app password generat
   - `NOTIFICATION_EMAIL`: unde să primești notificările

### 📱 Pas 4: Telegram Bot (Opțional)

1. Vorbește cu [@BotFather](https://t.me/botfather) pe Telegram
2. Creează bot nou: `/newbot`
3. Copiază **token-ul** și adaugă-l ca `TELEGRAM_BOT_TOKEN`
4. Pentru Chat ID:
   ```bash
   # Trimite un mesaj bot-ului, apoi accesează:
   https://api.telegram.org/bot<TOKEN>/getUpdates
   # Caută "chat":{"id":XXXXXX
   ```
5. Adaugă Chat ID ca `TELEGRAM_CHAT_ID`

---

## 🎯 Configurare Avansată

### 🔒 Acces Automat la Repo-uri Private

Workflow-ul poate acorda automat acces la repo-uri private pentru sponsori. Editează în workflow:

```yaml
# În secțiunea Auto-Grant Repository Access
repos_to_grant=("mvx-proofmind" "carbonflow-ai" "your-private-repo")
```

### 🎚️ Niveluri de Sponsorizare

- **Tier 1 ($5+)**: Acces la repo-uri private selectate
- **Tier 2 ($25+)**: Status VIP + beneficii suplimentare
- **Custom**: Beneficii personalizate

### ⏰ Programare Workflow

```yaml
# Configurează frecvența în workflow:
schedule:
  - cron: '0 */6 * * *'  # La fiecare 6 ore
  - cron: '0 9 * * *'    # Zilnic la 9:00
  - cron: '0 */1 * * *'  # La fiecare oră
```

---

## 📊 Monitorizare și Debug

### 🔍 Verificare Manuală

Poți rula workflow-ul manual:
1. Mergi la **Actions** tab în repo
2. Selectează "🎯 Monitor GitHub Sponsors"
3. Click **Run workflow**

### 📈 Statistici Disponibile

Workflow-ul creează fișiere cu statistici în `.sponsors-data/`:
- `current-sponsors.json` - Lista actuală de sponsori
- `previous-sponsors.json` - Lista anterioară (pentru comparație)
- `stats.json` - Statistici generale

### 🐛 Troubleshooting

**Workflow nu se execută:**
- Verifică că repo-ul este public sau ai GitHub Pro
- Asigură-te că workflow-ul este în branch-ul `main`

**Nu primești notificări:**
- Verifică că secretele sunt configurate corect
- Testează webhook-urile manual
- Uită-te în **Actions** logs pentru erori

**Token expirat:**
- PAT-urile au durată limitată
- Regenerează și actualizează secretul `GH_PAT`

---

## 🎨 Personalizare Notificări

### Discord Embeds
```json
{
  "embeds": [{
    "title": "🎉 Sponsor Nou!",
    "description": "@username tocmai a devenit sponsor!",
    "color": 3447003,
    "thumbnail": {
      "url": "https://github.com/username.png"
    }
  }]
}
```

### Email Templates
```html
<div style="font-family: Arial; max-width: 600px;">
  <h2 style="color: #28a745;">🎉 Sponsor Nou!</h2>
  <p>Detalii sponsor: <strong>@username</strong></p>
  <p>Tier: <strong>$X/lună</strong></p>
</div>
```

---

## 📚 Resurse Utile

- 📖 [GitHub Sponsors API](https://docs.github.com/en/rest/sponsors)
- 🔧 [GitHub Actions Docs](https://docs.github.com/en/actions)
- 💬 [Discord Webhooks](https://discord.com/developers/docs/resources/webhook)
- 📧 [Gmail SMTP Setup](https://support.google.com/mail/answer/7126229)
- 🤖 [Telegram Bot API](https://core.telegram.org/bots/api)

---

## 🚀 Status

- ✅ **Workflow**: Activ și funcțional
- ✅ **Monitorizare**: La fiecare 6 ore
- ✅ **Notificări**: Configurate pentru Discord, Email, Telegram
- ✅ **Acces automat**: Configurat pentru repo-uri private
- ✅ **Statistici**: Actualizate automat

---

*Sistemul este 100% gratuit și rulează pe GitHub Actions. Perfect pentru dezvoltatorii care vor să automatizeze gestionarea sponsorilor! 🎯*
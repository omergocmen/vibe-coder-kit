<div align="center">

# ⚡ Vibe Coder Kit

<!-- yarkr:badges:start -->
[![Indexed on Yarkr](https://api.yarkr.com/functions/v1/api/api/v1/badges/repos/omergocmen/vibe-coder-kit/version.svg)](https://yarkr.com/arks/omergocmen/vibe-coder-kit)
<!-- yarkr:badges:end -->

**AI Destekli Profesyonel Yazılım Geliştirme Agent Framework'ü**

*AI kod asistanını disiplinli, süreç odaklı bir geliştirme ekibine dönüştürün.*

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![OpenCode Compatible](https://img.shields.io/badge/OpenCode-Compatible-purple.svg)](https://opencode.ai)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)](#katkıda-bulunmak)

</div>

---

## 🎯 Vibe Coder Kit Nedir?

Vibe Coder Kit, AI kod asistanlarını (ör. [OpenCode](https://opencode.ai)) yapılandırılmış, süreç odaklı bir geliştirme ekibine dönüştüren **yapılandırma odaklı bir agent framework'üdür**. Anlık prompt yazmak yerine, şunlara sahip olursunuz:

- 🤖 **4 Uzman Agent Personalası** — Tasarımcı, Frontend Geliştirici, Backend Geliştirici, DevOps
- 🛠️ **12 Kanıtlanmış Skill** — Fikir üretiminden kriz yönetimine yapılandırılmış iş akışları
- 📏 **3 Kural Seti** — Kod hijyeni, kalite ve güvenlik standartları
- 🧠 **Kalıcı Bilgi Tabanı** — Oturumlar arası bilgi paylaşımı, tekrarlanan hataları önler

> **"Çalışıyor" ≠ "Bitti".** Testler geçiyor + temiz kod + dokümantasyon güncel = bitti.

---

## ✨ Öne Çıkan Özellikler

### 🎭 Agent Personalaları

| Agent | İsim | Uzmanlık Alanı |
|-------|------|---------------|
| 🎨 **Tasarımcı** | Aria | UI/UX, motion design, tasarım sistemleri, erişilebilirlik |
| 💻 **Frontend** | Felix | React/Vue, CSS mimarisi, performans, Core Web Vitals |
| ⚙️ **Backend** | Bora | API tasarımı, veritabanları, auth, güvenlik, mikroservisler |
| 🚀 **DevOps** | Deva | Docker, CI/CD, cloud altyapı, izleme, kriz yönetimi |

<!-- Her agent, kendi alanında senior seviye uzman olarak tasarlanmıştır. Detaylı bilgi için .agent/agents/ dizinine bakabilirsiniz. -->

### 🛠️ Skill'ler (Yapılandırılmış İş Akışları)

| Skill | Ne Zaman Kullanılır | Ne Yapar |
|-------|---------------------|----------|
| `project-context-primer` | Her oturum başında *(zorunlu)* | Proje bağlamını, kararları ve tuzakları yükler |
| `prompt-enhancer` | Belirsiz veya eksik istekler | Kapsamı netleştirir, eksik boyutları tamamlar |
| `brainstorming` | Yeni özellik veya proje fikirleri | Sokratik yöntemle rafine eder → scope dokümanı üretir |
| `writing-plans` | Scope onayından sonra | Checkpoint'li implementasyon planı oluşturur |
| `architecture-review` | Kod yazmaya başlamadan önce | Planı stres testine tabi tutar, riskleri işaretler |
| `test-driven-execution` | Her özellik implementasyonunda | Test önce, kod sonra yaklaşımı uygular |
| `code-review` | Her commit öncesinde | Pre-commit checklist + geri bildirim yanıtlama |
| `github` | Tüm git işlemlerinde | Conventional commits, branch yönetimi, PR iş akışı |
| `knowledge-base-update` | Önemli bir şey öğrenildiğinde | Oturumlar arası kalıcı bilgi depolama |
| `documentation-sync` | Önemli kod değişikliklerinden sonra | Dokümantasyon ve kodun uyumunu sağlar |
| `dependency-audit` | Release öncesi / aylık rutin | Güvenlik açıklarını ve eski paketleri tarama |
| `incident-response` | Production sorunlarında | Triyaj → içerme → düzeltme → post-mortem |

<!-- Skill'ler bağımsız olarak kullanılabilir, ancak tam verim için önerilen sırayla çalıştırılmalıdır. -->

### 📏 Kurallar (Zorunlu Standartlar)

| Kural | Amacı |
|-------|-------|
| `code-hygiene` | Yorum stili, debug log temizliği, hassas veri yönetimi |
| `code-quality` | Aşırı mühendislik yapmadan DRY, soyutlama eşiği |
| `safety` | Yıkıcı komut onayı, rollback planları |

<!-- Kurallar öneri değil, zorunluluktur. Agent bu kuralları her görevde uygular. -->

---

## 🚀 Kurulum ve Kullanım

Vibe Coder Kit'i iki şekilde kullanabilirsiniz: **mevcut projenize entegre ederek** veya **yeni bir proje olarak başlatarak**.

### Yöntem 1: Mevcut Projenize Entegre Etme (Önerilen)

Mevcut bir projeniz varsa, sadece agent yapılandırma dosyalarını projenize kopyalayın:

```bash
# 1. Repoyu indirin (geçici bir klasöre)
git clone https://github.com/omergocmen/vibe-coder-kit.git /tmp/vibe-coder-kit

# 2. .agent dizinini projenize kopyalayın
cp -r /tmp/vibe-coder-kit/.agent /projenizin/yolu/

# 3. OpenCode yapılandırma dosyasını kopyalayın
cp /tmp/vibe-coder-kit/opencode.json /projenizin/yolu/

# 4. AGENTS.md dosyasını kopyalayın (OpenCode bunu otomatik okur)
cp /tmp/vibe-coder-kit/AGENTS.md /projenizin/yolu/

# 5. Geçici dosyaları temizleyin
rm -rf /tmp/vibe-coder-kit

# 6. Proje dizinine gidin
cd /projenizin/yolu
```

**Windows (PowerShell) kullanıcıları:**

```powershell
# 1. Repoyu indirin
git clone https://github.com/omergocmen/vibe-coder-kit.git "$env:TEMP\vibe-coder-kit"

# 2. .agent dizinini projenize kopyalayın
Copy-Item -Recurse "$env:TEMP\vibe-coder-kit\.agent" "C:\projenizin\yolu\.agent"

# 3. Yapılandırma dosyalarını kopyalayın
Copy-Item "$env:TEMP\vibe-coder-kit\opencode.json" "C:\projenizin\yolu\"
Copy-Item "$env:TEMP\vibe-coder-kit\AGENTS.md" "C:\projenizin\yolu\"

# 4. Geçici dosyaları temizleyin
Remove-Item -Recurse "$env:TEMP\vibe-coder-kit"
```

### Yöntem 2: Yeni Proje Olarak Başlatma

Sıfırdan yeni bir proje başlatıyorsanız, repoyu doğrudan klonlayıp üzerine inşa edin:

```bash
# Repoyu klonlayın
git clone https://github.com/omergocmen/vibe-coder-kit.git benim-projem
cd benim-projem

# Artık .agent/, opencode.json ve AGENTS.md hazır
# Kendi kodunuzu bu dizin yapısının üzerine ekleyin
```

### İndirdikten Sonra Ne Yapmalısınız?

1. **[OpenCode](https://opencode.ai) kurun** — Henüz kurmadıysanız:
   ```bash
   # npm ile global kurulum
   npm install -g opencode
   
   # veya doğrudan çalıştırın
   npx opencode
   ```

2. **Proje dizininde OpenCode'u başlatın:**
   ```bash
   cd /projenizin/yolu
   opencode
   ```

3. **İlk oturumda** OpenCode otomatik olarak `AGENTS.md` dosyasını okuyacak ve `project-context-primer` skill'ini çalıştıracaktır. Agent size proje hakkında sorular soracak ve bağlamı yükleyecektir.

4. **Bilgi tabanını başlatın** — İlk oturumda `.agent/knowledge/INDEX.md` dosyası oluşturulur. Bundan sonra tüm kararlar, kurallar ve tuzaklar otomatik olarak kaydedilir.

### Yapıyı Özelleştirme

Projenize özel özelleştirmeler yapabilirsiniz:

- **Agent personalarını düzenleyin:** `.agent/agents/` dizinindeki dosyaları projenizin ihtiyacına göre değiştirin
- **Yeni skill ekleyin:** `.agent/skills/yeni-skill/SKILL.md` oluşturun
- **Kuralları sıkılaştırın:** `.agent/rules/` dizinindeki dosyaları düzenleyin
- **Gereksiz agent'ları kaldırın:** Örneğin sadece backend geliştirme yapıyorsanız, `designer.md` ve `frontend-dev.md` dosyalarını silebilirsiniz

<!-- Her projenin ihtiyacı farklıdır. Framework'ü projenize göre özelleştirmekten çekinmeyin. -->

---

## 📁 Proje Yapısı

```
vibe-coder-kit/
├── AGENTS.md                          # Oturum başlatma talimatları (OpenCode tarafından otomatik okunur)
├── opencode.json                      # OpenCode yapılandırma dosyası
├── .agent/
│   ├── agents/                        # Uzman personaları
│   │   ├── designer.md                # Aria — UI/UX ve motion design
│   │   ├── frontend-dev.md            # Felix — Frontend mühendisliği
│   │   ├── backend-dev.md             # Bora — Backend ve sistemler
│   │   └── devops.md                  # Deva — Altyapı ve operasyonlar
│   ├── skills/                        # Yapılandırılmış iş akışları
│   │   ├── project-context-primer/    # Oturum başlatma (zorunlu)
│   │   ├── prompt-enhancer/           # İstek netleştirme
│   │   ├── brainstorming/             # Sokratik tasarım rafinasyonu
│   │   ├── writing-plans/             # İmplementasyon planlama
│   │   ├── architecture-review/       # Plan stres testi
│   │   ├── test-driven-execution/     # TDD iş akışı
│   │   ├── code-review/               # Commit öncesi inceleme
│   │   ├── github/                    # Git işlemleri ve commit'ler
│   │   ├── knowledge-base-update/     # Kalıcı bellek
│   │   ├── documentation-sync/        # Dokümantasyon senkronizasyonu
│   │   ├── dependency-audit/          # Güvenlik taraması
│   │   └── incident-response/         # Kriz yönetimi
│   ├── rules/                         # Zorunlu standartlar
│   │   ├── code-hygiene.md            # Temiz kod kuralları
│   │   ├── code-quality.md            # DRY ve soyutlama kuralları
│   │   └── safety.md                  # Yıkıcı işlem güvenlikleri
│   └── knowledge/                     # Oturumlar arası bellek (otomatik doldurulur)
├── .kilo/                             # Planlama çalışma alanı
│   └── plans/
├── LICENSE
└── README.md
```

---

## 🔄 Geliştirme İş Akışı

```
🆕 YENİ OTURUM
  └─ project-context-primer (zorunlu)

💡 FİKİR     → brainstorming → SCOPE-<slug>.md
📋 PLAN      → writing-plans → implementation_plan.md → architecture-review
🛠️ GELİŞTİR  → test-driven-execution
✅ KOMİT     → code-review → github skill (conventional commits)
```

<!-- Bu iş akışı öneridir. Projenizin ihtiyacına göre adımları atlayabilir veya özelleştirebilirsiniz. -->

### Örnek Akış

1. **Oturum başlat** → `project-context-primer` bağlamı yükler
2. **Özelliği tanımla** → `brainstorming` bir scope dokümanı üretir
3. **İmplementasyonu planla** → `writing-plans` checkpoint'li plan oluşturur
4. **Mimariyi incele** → `architecture-review` planı stres testine tabi tutar
5. **Geliştir** → `test-driven-execution` ile implementasyon yapılır
6. **Kodu incele** → `code-review` pre-commit checklist çalıştırır
7. **Commit ve push** → `github` skill conventional commits ve PR'ları yönetir

---

## 🧠 Bilgi Kalıcılığı

En güçlü özelliklerden biri. Her önemli karar, tuzak, kural ve bug köken nedeni `.agent/knowledge/` dizininde saklanır ve oturum başlangıcında otomatik yüklenir:

| Tür | Ne Saklanır |
|-----|-------------|
| `decision` | Mimari seçimler, teknoloji tercihler ve gerekçeleri |
| `convention` | İsimlendirme kuralları, kod pattern'leri, klasör yapıları |
| `bug` | Belirsiz sorunların köken nedeni ve çözümü |
| `gotcha` | 3. parti servis tuzakları, ortam sorunları, edge case'ler |
| `research` | Önemli araştırma gerektiren soruların cevapları |

<!-- Aynı sorunları her oturumda yeniden keşfetmek zorunda kalmazsınız. Bilgi birikir ve aktarılır. -->

---

## 🤝 Uyumluluk

**[OpenCode](https://opencode.ai)** için geliştirilmiştir, ancak kavramlar taşınabilir:

| Araç | Nasıl Kullanılır |
|------|-----------------|
| **OpenCode** | `opencode.json` + `AGENTS.md` ile doğal destek |
| **Cursor** | Agent personalarını custom instructions olarak kullanın |
| **Claude Code** | Skill dosyalarını `CLAUDE.md` içinde referans verin |
| **GitHub Copilot** | Kuralları custom instructions'a uyarlayın |
| **Windsurf** | Personaları agent yapılandırması olarak yükleyin |

---

## 📋 Conventional Commits

Bu kit [Conventional Commits](https://www.conventionalcommits.org/) standardını uygular:

```
feat(auth): add refresh token rotation
fix(userService): handle null email in validation
refactor(Button): extract loading state to hook
docs(readme): update installation instructions
chore(deps): upgrade react to 19.2.0
```

<!-- Commit mesajları İngilizce yazılır, emir kipinde (imperative mood) olmalıdır. Detaylar için .agent/skills/github/SKILL.md dosyasına bakın. -->

---

## 🌐 Dil Tercihi

Tüm agent talimatları, kurallar ve skill dokümantasyonu **Türkçe** yazılmıştır. İngilizce frontmatter ile birlikte sunulur. Bu Türkçe konuşan geliştirme ekipleri için bilinçli bir tercihtir. Çeviri katkılarına açığız.

---

## 🤝 Katkıda Bulunmak

Katkılar memnuniyetle karşılanır! Mevcut yapıyı takip edin:

1. Repo'yu fork edin
2. Özellik branch'i oluşturun: `feat/yeni-ozellik`
3. Mevcut skill/agent/rule yapısına uygun değişiklik yapın
4. Pull request gönderin

### Yeni Skill Eklemek

`.agent/skills/skill-adi/SKILL.md` dosyası oluşturun:

```markdown
---
name: skill-adi
description: >
  Bu skill ne zaman kullanılır ve ne üretir.
---

# Skill Adı

## Ne Zaman Tetiklenir
## Adım Adım Süreç
## Kurallar
```

### Yeni Agent Personalası Eklemek

`.agent/agents/agent-adi.md` dosyası oluşturun:

```markdown
# Agent: Agent Adı

## Kimlik
## Uzmanlık Alanları
## Çalışma Metodolojisi
## Kod Standartları
## Asla Yapma
## Kullanılan Skill'ler
```

---

## 📄 Lisans

Bu proje MIT Lisansı ile lisanslanmıştır. Detaylar için [LICENSE](LICENSE) dosyasına bakın.

---

## 🌟 Destek

Bu kit geliştirme iş akışınızı iyileştirdiyse:

- ⭐ Bu repo'yu star'layın
- 🐛 Sorunları bildirin (Issues sekmesi)
- 💡 Yeni skill veya agent personalası önerin
- 🔀 Pull request gönderin

---

<div align="center">

**⚡ ile geliştirildi by [omer gocmen](https://github.com/omergocmen)**

*Sadece çalışan değil — kalıcı yazılım geliştirin.*

</div>

<!-- yarkr:install:start -->
## Install with Yarkr

This repo is indexed on [Yarkr](https://yarkr.com/arks/omergocmen/vibe-coder-kit) as the ark [omergocmen/vibe-coder-kit](https://yarkr.com/arks/omergocmen/vibe-coder-kit), so its skills install into Claude Code, Codex, Cursor and other agent harnesses with one command.

### CLI

Install the whole ark, which Yarkr keeps equal to this repo:

```bash
npx yarkr-cli sync omergocmen/vibe-coder-kit
```

Or add individual skills:

```bash
npx yarkr-cli add skill:omergocmen/vibe-coder-kit/architecture-review
npx yarkr-cli add skill:omergocmen/vibe-coder-kit/code-review
npx yarkr-cli add skill:omergocmen/vibe-coder-kit/dependency-audit
```

No Node.js? `curl -fsSL https://yarkr.com/install.sh | sh` (macOS, Linux) or `irm https://yarkr.com/install.ps1 | iex` (Windows PowerShell) installs `yarkr` as a standalone binary; then type `yarkr` in place of `npx yarkr-cli`.

### MCP

Connect your agent to the ark over MCP:

```bash
npx yarkr-cli mcp add omergocmen/vibe-coder-kit
```

Or point any MCP client at `https://api.yarkr.com/functions/v1/api/mcp/o/omergocmen/vibe-coder-kit`.
<!-- yarkr:install:end -->

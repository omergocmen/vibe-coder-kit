<!--
  TÜRKÇE AÇIKLAMA
  ───────────────
  Bu skill, onaylanmış bir scope veya fikirden somut, uygulanabilir bir
  implementasyon planı üretir. Hangi dosya değişecek, hangi sırayla, kim yapacak,
  ne kadar sürecek, hangi riskler var — hepsini netleştirir. Planın çıktısı
  doğrudan `executing-plans` veya `dispatching-parallel-agents` skilllerine girer.

  NE ZAMAN: Brainstorming tamamlandıktan ve scope onaylandıktan sonra,
            kod yazmaya başlamadan önce.
  ÇIKTI:    implementation_plan.md — checkpoint'li, bağımlılık sıralı, riskli adımlar işaretli.
-->

---
name: writing-plans
description: >
  Turns an approved scope or idea into a concrete, executable implementation plan.
  Defines what changes, in what order, with what dependencies, risks flagged,
  and checkpoints marked. Output feeds directly into executing-plans or
  dispatching-parallel-agents.
---

# Writing Plans Skill

## Ön Koşul

Bu skill başlamadan önce şunlar hazır olmalı:
- [ ] `brainstorming` tamamlandı ve scope doc var → `.agent/SCOPE-<slug>.md`
- [ ] Başarı kriterleri netleşti
- [ ] Tech stack kararı verildi

**Scope doc'u yükle:** `.agent/SCOPE-*.md` patterninde arama yap ve en son tarihli olanı oku.
Bunlar yoksa önce `brainstorming` skill'ini çalıştır.

---

## Süreç

### Adım 1: Etkilenen Alanları Haritala

Mevcut kod tabanını tara ve neyin değişeceğini belirle:

```
src/
├── components/     ← Yeni komponent: UserCard
├── services/       ← Değişecek: userService.ts
├── api/            ← Yeni endpoint: POST /api/users
├── db/migrations/  ← Yeni migration: add_users_table
└── tests/          ← Yeni testler: userService.test.ts
```

Her etkilenen dosya için:
- **Yeni mi, değişiyor mu, siliniyor mu?**
- **Başka ne bu dosyaya bağımlı?** (kırmadan değiştirilebilir mi?)

---

### Adım 2: Görevleri Atomik Parçalara Böl

Her görev:
- **Tek bir şey** yapar
- **Bağımsız** commit olabilir
- **Test edilebilir** (tamamlandığını nasıl anlarsın?)
- **2 saatten kısa** (daha uzunsa böl)

```markdown
## Görev Listesi

### T1: Database migration — users tablosu
- Dosya: db/migrations/001_create_users.sql
- İçerik: id, email, password_hash, created_at, deleted_at
- Bağımlılık: Yok (ilk adım)
- Test: Migration up/down çalışıyor

### T2: User model ve repository
- Dosya: src/db/repositories/userRepository.ts
- İçerik: findById, findByEmail, create, softDelete
- Bağımlılık: T1 (migration olmalı)
- Test: repository unit testleri geçiyor

### T3: UserService — iş mantığı
- Dosya: src/services/userService.ts
- İçerik: createUser (hash password), getUser, deleteUser
- Bağımlılık: T2
- Test: service unit testleri geçiyor

### T4: API endpoint — POST /api/users
- Dosya: src/api/routes/users.ts
- İçerik: validation, auth middleware, service çağrısı
- Bağımlılık: T3
- Test: integration test geçiyor

### T5: Frontend — UserCard komponenti
- Dosya: src/components/UserCard/
- İçerik: komponent + test + storybook
- Bağımlılık: T4 (API mock veya gerçek)
- Test: komponent testleri geçiyor
```

---

### Adım 3: Bağımlılık Grafiği Çiz

```
T1 (migration)
  └── T2 (repository)
        └── T3 (service)
              └── T4 (API endpoint)
                    └── T5 (frontend)
```

**Paralel çalışabilecek görevler** ayrı kollar olarak işaretle:
```
T1
├── T2 → T3 → T4 (backend kolu)
└── T5-mock (frontend kolu — mocked API ile başlayabilir)
```

---

### Adım 4: Risk ve Checkpoint'leri İşaretle

Her görevin yanına:
- `[RISK]` — başarısız olursa diğerleri bloke olur
- `[CHECKPOINT]` — bu noktada pause edilebilir, sonuç doğrulanabilir
- `[BREAKING]` — mevcut kodu kırar, dikkat gerekir
- `[PARALLEL]` — başka görevle aynı anda yapılabilir

```markdown
### T3: UserService [RISK] [CHECKPOINT]
Bu görev tüm backend'in temelini oluşturuyor.
Burada durup review yapılmalı, sonra API katmanına geçilmeli.
```

---

### Adım 5: Planı Yaz

`implementation_plan.md` dosyasına yaz:

```markdown
# Implementation Plan: <proje adı>
**Tarih:** <YYYY-MM-DD>  
**Tahmini Süre:** <X gün/saat>
**Kaynak:** [Scope Doc](.agent/SCOPE-<slug>.md)

## Özet
<2-3 cümle: ne yapılacak, nasıl yapılacak>

## Tech Stack Kararları
| Alan | Seçim | Gerekçe |
|------|-------|---------|
| ORM | Prisma | Type-safe, migration yönetimi iyi |
| Auth | JWT + refresh token | Stateless, ölçeklenebilir |

## Görevler

### 🔵 Aşama 1: Temel (Paralel çalışmaz)
- [ ] **T1:** Database migration `[CHECKPOINT]`
- [ ] **T2:** Repository katmanı

### 🟡 Aşama 2: Çekirdek (T1 ve T2 bitince)
- [ ] **T3:** Service katmanı `[RISK][CHECKPOINT]`
- [ ] **T4:** API endpoint `[BREAKING]`

### 🟢 Aşama 3: UI (T4 veya mock hazırken)
- [ ] **T5:** Frontend komponent `[PARALLEL]`

## Risk Listesi
| Risk | Olasılık | Etki | Önlem |
|------|----------|------|-------|
| Migration geri alınamaz | Düşük | Yüksek | Down migration yaz ve test et |

## Tanımlanmamış Noktalar
- [ ] Email doğrulama akışı: gerekli mi? (karar bekleniyor)

## Sonraki Adım
1. `architecture-review` skill'ini çalıştır — plan onaylanmadan kod başlamaz
2. Onaydan sonra `executing-plans` veya `dispatching-parallel-agents`
```

---

## Kurallar

- **Her görev test kriteriyle biter.** "Tamamlandı" = testler geçiyor.
- **Hiçbir görev "ve ayrıca" içermez.** Varsa böl.
- **"Sonra hallederiz" plan'a girmez.** Ya göreve dönüştür ya scope dışına at.
- **Plan değişirse güncellenir.** Eski plan geçerliliğini yitirir — silme, tarih ver.
- **`architecture-review` atlanamaz.** Özellikle `[RISK]` işaretli görevler varsa zorunludur.

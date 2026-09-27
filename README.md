# Geoproje eklentisi (Claude)

[Türkçe](#türkçe) | [English](#english)

## Türkçe

### Ne yapar

Bu eklenti Geoproje mühendislik araçlarını Claude'a bağlar. İki parçadan oluşur:

- **Geoproje bağlayıcısı** (`https://mcp.geoproje.com.tr/mcp`): Geoproje hesabınızla
  bağlanan uzak MCP sunucusu. Zemin etüdü profillerini okur, modül proje dosyası
  hazırlar, TBDY 2018 tehlike spektrumunu verir ve SelectEQ, GMPS, GeoWave, OmniPile,
  Hoek-Brown ve PMM hesap uçlarını çağırır.
- **Yönlendirici skill** (`geoproje-engineering-assistant`): Claude'a hangi iş için
  hangi Geoproje aracının kullanılacağını söyler. Claude'un izlediği talimatların
  tamamı bu depodaki skill dosyasındadır; eklenti sunucudan talimat indirmez.

### Kimin için

Geoteknik ve deprem mühendisliği yapan mühendisler ve firmalar: zemin etüdü,
sahaya özel zemin davranışı analizi (SOZDA), deprem kaydı seçimi ve benzeştirme,
kazık taşıma gücü, geoteknik rapor hazırlama ve inceleme.

### Kurulum

- **Claude (web, masaüstü, Cowork):** Customize > Plugins bölümünde Geoproje
  eklentisini ekleyin. Sonra eklentinin Connectors sekmesinden Geoproje
  bağlayıcısını bağlayın ve Geoproje hesabınızla giriş yapın.
- **Claude Code:** `/plugin` menüsünden eklentiyi kurun. Dizinde listelenene kadar
  depo bir marketplace olarak da eklenebilir:
  `/plugin marketplace add ozanbilal/geoproje-claude-plugin` ve `/plugin install geoproje@geoproje`.
  Bağlantı durumunu `/mcp` ile görün.

### Geoproje hesabı

- Bağlayıcı bir Geoproje hesabı ve **ücretli bir plan** ister. Free hesap bağlayıcıyı
  bağlayamaz; bağlanma sırasında "API anahtarı için ücretli bir plan gerekir" mesajı
  görünür. Free hesapla araçları app.geoproje.com.tr üzerinden tarayıcıda
  kullanabilirsiniz.
- Ücretli planlar modül paketleri (SelectEQ, GMPS, GeoWave, OmniPile, Hoek-Brown,
  PMM) ve tüm araçları açan All-Access planıdır. Her paket kendi aracını açar.
  All-Access planı aya dahil bir API kredisi içerir; hak bitince işler kredi
  bakiyenizden düşer.
- Bazı işlemler kredi harcar: ücretli hesap uçları (`arac_kos`), etüt çıkarımı ve
  Geoproje asistanına soru (`asistana_sor`). Claude kredi harcayan bir adımdan önce
  onayınızı ister. Güncel fiyatlar ve planlar: https://app.geoproje.com.tr/planlar
- Plan ve modül kontrolü Geoproje sunucusunda yapılır. Planınızda olmayan bir araç
  çağrılırsa bağlayıcı kısa bir hata ve plan sayfası bağlantısı döner.

### Örnek istemler

1. "Hesabımda hangi modüller açık ve kredi bakiyem ne kadar?"
2. "Kahramanmaraş Pazarcık (37,49 K, 37,29 D) için TBDY 2018 DD-2 ve ZC zemin
   sınıfında tasarım spektrumunu getir, sonra bu hedefe göre SelectEQ ile 11 kayıtlık
   bir seçim hazırla. Kredi harcamadan önce bana sor."
3. "Etütlerim'e yüklediğim son etüdün zemin profilini getir, eksik ve onaysız
   satırları listele, GeoWave proje dosyasını hazırla ve Proje Dosyalarıma kaydet."
4. "Biten SelectEQ seçimimin kayıt listesini kaynak sayfaları ve atıf metinleriyle
   ver, GMPS proje dosyasını da hesabıma kaydet."
5. "Proje Dosyalarımdaki son OmniPile dosyasını aç, kazık boyunu 2 m artırarak
   taşıma gücünü yeniden hesapla ve iki sonucu karşılaştır."

Etüt belgelerini (PDF, DWG, XLSX) app.geoproje.com.tr "Etütlerim" sayfasından
yükleyin. Uzak bağlayıcı bilgisayarınızdaki dosya yollarını okuyamaz.

### Gizlilik ve veri

- Bu eklenti kendi başına veri saklamaz ve başka bir yere veri göndermez.
- Bağlayıcıyı kullandığınızda Claude'un araç çağrılarındaki girdiler (koordinat,
  zemin sınıfı, etüt kimliği, hesap gövdesi, soru metni) Geoproje sunucularına
  (`mcp.geoproje.com.tr` ve Geoproje hesap servisi) gider ve hesabınızla ilişkilendirilir.
  Hesap uçları ilgili Geoproje modül sunucusunda çalışır; kullanım ve kredi hareketi
  hesabınıza kaydedilir.
- Giriş OAuth ile yapılır; parolanız Claude'a verilmez.
- Kişisel verilerin işlenmesi: https://app.geoproje.com.tr/gizlilik ve
  https://app.geoproje.com.tr/kullanim-kosullari

### Destek

https://app.geoproje.com.tr/iletisim

### Sorumluluk

Geoproje araçları ve Claude'un çıktıları mühendislik onayı değildir. Nihai tasarım,
yönetmelik yorumu ve rapor onayı yetkili mühendisin sorumluluğundadır.

## English

### What it does

This plugin connects Geoproje engineering tools to Claude. It has two parts:

- **Geoproje connector** (`https://mcp.geoproje.com.tr/mcp`): a remote MCP server you
  connect with your Geoproje account. It reads soil investigation profiles, prepares
  module project files, returns the TBDY 2018 hazard spectrum for sites in Turkey, and
  calls the SelectEQ, GMPS, GeoWave, OmniPile, Hoek-Brown and PMM compute endpoints.
- **Router skill** (`geoproje-engineering-assistant`): tells Claude which Geoproje tool
  fits each task. All instructions Claude follows are in the skill file in this
  repository; the plugin does not download instructions from a server.

### Who it is for

Geotechnical and earthquake engineers: soil investigations, site-specific site response
analysis, ground motion selection and spectral matching, pile capacity, and geotechnical
report writing and review.

### Install

- **Claude (web, desktop, Cowork):** add the Geoproje plugin in Customize > Plugins, then
  connect the Geoproje connector from the plugin's Connectors tab and sign in with your
  Geoproje account.
- **Claude Code:** install it from `/plugin`. Before the directory listing, you can add
  the repository as a marketplace: `/plugin marketplace add ozanbilal/geoproje-claude-plugin` and
  `/plugin install geoproje@geoproje`. Check the connection with `/mcp`.

### Geoproje account

- The connector needs a Geoproje account on a **paid plan**. A Free account cannot connect
  the connector. Free accounts can still use the tools in the browser at
  app.geoproje.com.tr.
- Paid plans are module packages (SelectEQ, GMPS, GeoWave, OmniPile, Hoek-Brown, PMM) and
  the All-Access plan. Each package opens its own tool. All-Access includes a monthly API
  credit allowance; after that, runs use your credit balance.
- Some operations spend credits: paid compute endpoints (`arac_kos`), document extraction
  and assistant questions (`asistana_sor`). Claude asks for your confirmation first.
  Current prices and plans: https://app.geoproje.com.tr/planlar
- Plan and module checks happen on the Geoproje server. If a tool is not in your plan, the
  connector returns a short error with a link to the plans page.

### Example prompts

1. "Which modules are active on my account and what is my credit balance?"
2. "Get the TBDY 2018 DD-2 design spectrum for site class ZC at Pazarcık, Kahramanmaraş
   (37.49 N, 37.29 E), then prepare an 11-record SelectEQ selection for that target. Ask
   me before spending credits."
3. "Get the soil profile of the last study I uploaded to Etütlerim, list missing and
   unconfirmed rows, prepare the GeoWave project file and save it to my project files."
4. "List the records of my finished SelectEQ selection with source pages and citations,
   and save the GMPS project file to my account."
5. "Open my latest OmniPile project file, recompute the pile capacity with the pile 2 m
   longer and compare the two results."

Upload study documents (PDF, DWG, XLSX) on the Etütlerim page at app.geoproje.com.tr. The
remote connector cannot read file paths on your computer.

### Privacy and data

- The plugin itself stores no data and sends no data anywhere.
- When you use the connector, the inputs of Claude's tool calls (coordinates, site class,
  study id, compute request body, question text) go to Geoproje servers
  (`mcp.geoproje.com.tr` and the Geoproje account service) and are linked to your account.
  Compute requests run on the matching Geoproje module server; usage and credit movements
  are recorded on your account.
- Sign-in uses OAuth; Claude never receives your password.
- Personal data processing: https://app.geoproje.com.tr/gizlilik and
  https://app.geoproje.com.tr/kullanim-kosullari

### Support

https://app.geoproje.com.tr/iletisim

### Disclaimer

Geoproje tools and Claude's outputs are not an engineering approval. Final design, code
interpretation and report approval remain the responsibility of the engineer of record.

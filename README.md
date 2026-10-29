# VUM hisobot tizimi: tayyor fayllar (2026-10-29)

Bu papkada **13 ta fayl** bor. Ularning har biri Apps Script'dagi **shu nomli faylning o'rniga** qo'yiladi. Qolgan fayllar (Code, DASH, Instagram, OylikForma, Prognoz, RejaBot, Sayt, SEO, Telegram, Tezlik, YouTube) o'zgarmagan, ularga tegmang.

Hamma 25 fayl birga sintaksis bo'yicha tekshirildi: xato yo'q, takroriy nom yo'q (358 ta nom). Jonli ma'lumotda hali ishlatilmagan: birinchi tekshiruv quyidagi qadamlar.

## Fayllarni qo'yish (har bir fayl uchun)
1. Apps Script → chapdan faylni oching (masalan AmoCRM.gs).
2. Ctrl+A → Delete (eski matn to'liq o'chsin).
3. Shu papkadagi faylni Notepad'da ochib, Ctrl+A → Ctrl+C → Apps Script'ga Ctrl+V.
4. Ctrl+S. Qizil xato chiziq bo'lmasligi kerak.

13 ta fayl: AmoCRM, CallCenter, CrmDash, CrmPPT, CrmSync, Haftalik, KunlikAds, KunlikXulosa, MetaCAPI, MetaMoslik, Nazorat, PPT, Reklama.

Oxirida: Deploy → Manage deployments → ✏️ → Version: **New version** → Deploy.

## Bir martalik qadamlar (shu tartibda)
1. **Script Properties**: `LEADLAR_MANBA` bo'lsa, o'chiring. Keyin LEADLAR varag'ini "Statistik malumotlar → Call Center" bilan oyma-oy solishtiring; farq qilgan katakni qo'lda to'g'rilang.
2. **crmLidlarTarixQaytadan** → Run. CRM_LIDLAR ga "Voronka ID" va "Bosqich ID" ustunlari qo'shiladi (sarlavha o'zi yoziladi). 6 daqiqaga sig'masa, o'zi davom etadi. Tugashini kuting.
3. **moslikKampTuzat** → Run. MOSLIK dagi kampaniya ID lari tiklanadi, KAMPANIYA_CRM va KREATIV_CRM qayta quriladi.
4. **hrTekshir** → Run. Log'da faqat vakansiya kampaniyalari chiqishi kerak. Boshqa kampaniya chiqsa, menga yozing.
5. **crmTungiYoqish** → Run (trigger dublikati bo'lmasligi uchun). Keyin tekshiring: `Logger.log(ScriptApp.getProjectTriggers().map(t=>t.getHandlerFunction()).join(', '))` — `crmSinx` bo'lmasligi, jami 20 tadan kam bo'lishi kerak.
6. **metaTortish** → Run (B3 = 2026-09 qilib). REKLAMA'dagi sentyabr Meta lidlari Ads Manager "Results" bilan teng bo'lishi kerak.

## Audit tuzatishlari (Critical va High, P1–P13)
- Kampaniya ID matn sifatida saqlanadi (MOSLIK, KAMPANIYA_CRM).
- Meta lidi = Ads Manager "Results"; umumiy "lead" hech qachon olinmaydi.
- LEADLAR faqat call center faylidan (rasmiy raqam CRM bilan almashmaydi).
- "Meta manba" bitta qoida bilan hamma joyda (isMeta).
- CPL = Meta xarajat / Ads Manager lidi; PPT'dagi boshqa "CPL" lar to'g'ri nomlandi; xarajat o'zgarishi kulrang (neytral).
- Konversiya = sotuv / sifatli lid.
- Dushanba xabarida sifat qo'yilmagan lidlar 90% dan kam bo'lsa, CPQL va sifat "⏳ dastlabki" deb ko'rsatiladi, rang va tavsiya berilmaydi; bog'lanish foizi haqiqiy hisoblanadi.
- 08:00 xabaridan bir kunlik kampaniya CPQL olib tashlandi.
- Narx 0 bo'lsa "🟢 -100%" chiqmaydi.
- Meta hisobi vaqt zonasi Toshkent bo'lmasa ogohlantiradi.
- HR filtri so'z chegarasi bilan ("shahr_lead" endi chiqarib tashlanmaydi).
- Call center oyi yil bilan topiladi; bir oy nomi ikki marta bo'lsa xato beradi (sarlavhaga yil yozing: "Yanvar 2027").
- CRM_LIDLAR voronka va bosqich ID larini saqlaydi; filtrlar nom emas, ID bo'yicha.

## Qo'shimcha tuzatishlar (O'rtacha va Past)
- **#15** Oylik CRM xabarida joriy oy tugamagan bo'lsa, "⏳ Oy hali tugamagan" yoziladi va rangli solishtirish berilmaydi.
- **#18** CRM "aloqaga chiqilgan" bitta ta'rif bilan (PPT va LEADLAR_SOLISHTIR bir xil).
- **#19** CRM_OYLIK: lid yo'q, lekin sotuvi bor manbalar ham yoziladi; manba hamma joyda bitta qoida (yangi maydon, bo'lmasa eski).
- **#20** CAPI: har 200 lik to'p alohida log'ga yoziladi (xato bo'lsa takror yuborilmaydi); event_id qo'shildi (Meta dublikatni o'chiradi); faqat Meta va CRM vaqti 2 daqiqadan kam farq qilgan ishonchli juftlar yuboriladi.
- **#21** crmSinxYoqish endi crmTungiYoqish ga yo'naltiradi (ikki marta sinx bo'lmaydi).
- **#22** Har yakshanba kechasi CRM 14 kunlik o'zgarishlar bilan sinxronlanadi (triggerlar to'xtab qolsa ham tiklanadi).
- **#23** amoCRM 429 / 5xx / tarmoq uzilishida 3 marta qayta urinadi.
- **#27** 3900 belgidan uzun bitta qator ham bo'linadi.
- **#28** Haftalik ichidagi `TZ` nomi `TZh` ga o'zgartirildi.
- **#30** "Sifatlidan tashrif %" → "Tashrif / sifatli %".
- **#31** Call center faylida oy nomi aniqroq topiladi: "Yangi", "Marketing" oy deb olinmaydi, lekin fayldagi imlo xatolari ("Oktaybr", "August") ham taniladi. Haqiqiy fayl sarlavhalari bilan sinab ko'rildi.
- **PPT** 2-slayd: "Sotuvlar" kartasidagi yozuv "konversiya" emas, "sifatli → sotuv" (HISOBOT C12 endi sotuv / sifatli).
- **#32** Organik va HR lidlar KAMPANIYA_CRM ga qator bo'lib tushmaydi.

## Tuzatilmagan, siz qaror qilasiz
- **isMeta**: hozir manbada "meta", "instagram" yoki "facebook" bo'lsa Meta deb olinadi. CRM'da "Instagram" organik Instagram'ni bildirsa, CPQL ga ortiqcha lid kiradi. Tekshirish: Apps Script'da yangi funksiya yarating va ishga tushiring:
  `function manbaRoyxat(){const m={};crmQatorlar().filter(isCC).forEach(r=>{m[r[6]]=(m[r[6]]||0)+1});Logger.log(JSON.stringify(m,null,1));}`
  Natijani menga yuboring.
- **#16 valyuta**: Meta hisobi USD da bo'lsa muammo yo'q (bizda USD).
- **#17**: javob tezligi medianasi faqat ishlangan lidlar bo'yicha; ishlanmaganlar alohida ko'rsatiladi.
- **#25**: `tgAdminTopish` ni ishlatmang; TG_ADMIN_CHAT allaqachon to'g'ri.
- **#26**: call center fayli katagi bo'shatilsa, LEADLAR'da eski qiymat qoladi. Bunday holatda qo'lda tozalang.
- **#29**: ROMI kodda hisoblanadi, lekin hech qayerda ko'rsatilmaydi.

## Jadval (HISOBOT, LEADLAR) tekshiruvi, 2026-10-29
- HISOBOT'da formula xatosi (#REF!, #DIV/0!, #N/A) yo'q. ROMI qatori o'chirilgan; TEKSHIRUV varag'idagi 13 ta havola to'g'ri qatorlarga ko'rsatadi.
- C12/D12 (konversiya) = Sotuvlar / Sifatli: Sentyabr 4,2%, Avgust 3,2% ✅. B12 yorlig'i hali "Lead→sotuv konversiyasi"; xohlasangiz "Sifatli→sotuv konversiyasi" ga o'zgartiring, PPT ikkalasini ham taniydi.
- LEADLAR yanvar–sentyabr call center fayli bilan katakma-katak bir xil ✅.
- Call center faylining o'zida: yanvar–may "Aloqaga chiqilgan" = "Jami leadlar" (100%), yanvarda "Sifatli" bo'sh, mart "Javob bermagan" bo'sh, avgust konversiya katagi #DIV/0!. Bu call center rahbari to'ldiradigan qism, unga ayting.
- E ustuni (o'zgarish) foizli ko'rsatkichlarda nisbiy farqni ko'rsatadi (3,2% → 4,2% = +32%), punkt emas. Obunachi o'sishi manfiy bo'lsa (IG Servis -1 → -3) foiz ma'nosiz chiqadi (+200%).

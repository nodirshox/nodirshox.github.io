---
layout: post
title: "Algoritm haqida"
categories: ["programming", "tutorial", "algorithm"]
permalink: /algoritm-haqida
---

Algoritm nima? Algoritm bu ma’lum bir vazifani bajarishga qaratilgan kichik dastur. Algoritm tushunchasini kengroq qilib tushintirganda, berilgan masalani yechish uchun ketma-ketliklar majmuasidir.

![Algoritm](/assets/2020-07-17-algorithm/algorithm.jpg)

Algoritmni hayotimizda juda ko’p sohalarda ishlatiladi: chorraxada svetafor, binolarda lift. Hattoki o’zimiz oddiy hayotiy ishlarda ham algoritm ishlatamiz: choynakga choy damlash. Algoritmlarning komputer sohasida ham muhim ro’l o’ynaydi. Chunki, dasturchi yozgan dasturlar hammasi ma’lum bir ketma-ketlik bilan ishlaydi.

Keling algoritmni tushinish uchun misol tariqasida kichik masalani ko’rib chiqamiz:

**Masala**

Mehmonxonada joylashgan odamlar sonini aniqlang?

**Ma’lumot**

![Algoritm](/assets/2020-07-17-algorithm/algo-2.jpg)

**What’s an algorithm? – David J. Malan**

**Javob:** X ta

Asosan, masala berilganda quyidagilar taqdim etiladi: masala talablari va ‘Input’ ya’ni masala yechish uchun berilgan ma’lumot. Yuqoridagi misol keltirilgan masalada, masala sharti(odamlar sonini topish) va ma’lumot(rasm) berildi.

Yechim: Endi siz masalani hayolingizda qanday yechdingiz. Shu haqida o’ylab ko’ring.

Siz yuqori ehtimollik bilan odamlar sonini rasmga qarab bir kishilab sanab chiqdingiz. Masalan, 1, 2, 3 , 4, … . Demak, shu masalani yechish uchun “Pseudo code” ya’ni dasturlash tilida yozgandek oddiy matn orqali yozaylik:

```
N=0 o'zgaruvchi olaylik:
Agar xonada insonni ko'rsak:
    N=N+1
```

Keling yozganimizni batafsil ko’rib chiqaylik.

**1-qator**: N=0, dasturlash tilida “variable” ya’ni “o’zgaruvchi” tushinchasi mavjud. Bu o’zgaruvchi hohlagan raqam yoki so’z bo’lishi mumkin. Masalan,: X=0, odam_soni=0, …

**2-3 qator**: Har bir odamni ko’rganimizda yuqoridagi yozgan N o’zgaruvchimizni 1 soniga oshirib boramiz ya’ni N=N+1. Bu holat xonada bir odamni sanab bo’lganimizda yana takrorlanadi. Bu jaralonni ‘loop’ ya’ni o’zbekchada takrorlanuvchi halqa deb tushinchak bo’ladi.

Demak, tuzilgan algorimtni tekshirib ko’ramiz:

Masalan: Xonada 2 kishi bor.

Algoritmni ishga tushiramiz.

**1-qadam**

Odamlar sonini hisoblab boradigan o’zgaruvchini ya’ni N=0 ga tenglashtiramiz.

**2-qadam**

Xonada 1-odamni ko’rdik. 2-qatordagi shartimizni qanoatlantiradi va 3-qatorga o’tamiz.

**3-qadam**

N sonini 1 ga oshiramiz(N=N+1). N ning hozirgi qiymati 0 ga teng edi, shuning N ning yakuniy qiymat 1 ga teng bo’ladi:

N=N+1 ⇒

N=0+1 ⇒

N=1

**4-qadam**

Xonada sanalmagan inson qoldimi? -Ha, bir kishi. Demak hali odam bor, shuning uchun 2-qatordagi shartmizni yana ishlaydi va N qiymati yana birga oshadi.

N=N+1 ⇒

N=1+1 ⇒

N=2

**5-qadam**

Xona sanalmagan odam qoldimi? -Yo’q. Demak algoritm yakunlandi.

**Javob**: N=2

Algoritm javobi 2 ya’ni xonada 2 kishi bor ekan. Javob to’g’ri✅.

Quyida algoritm ishlashini animation ko’rishda ko’ringiz mumkin.

<iframe src="https://giphy.com/embed/KEjbqMqanmMII4mz2E" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

**Algoritm ishlashi animatsion ko’rinishda**

Masalani endi boshqa ko’rinishda ya’ni xonadagi odamlar sonini o’zgartirgan holatda ko’rib chiqamiz.

**Masala**: Tasavvur qiling xonada odam yo’q.

?Algoritmni ishga tushiramiz.

**1-qadam**

Odamlar sonini hisoblab boradigan o’zgaruvchini ya’ni N=0 ga tenglashtiramiz.

**2-qadam**

Xonada odam bormi? – Yo’q. Demak, 2-qatorda yozilgan shartni qanoatlantirmaydi va algoritm 2-3 qatorni o’tkazib yuboradi.

(*Bu hodisa yuqoridagi masaladek qayta takrorlanmaydi. Chunki xonada sanashga odam yo’q)

**3-qadam**

Algoritm yakunladi. N=0

**Javob**: N=0

Yakunda, N sonimiz o’zgarmay qoldi va qiymati N=0 ga teng. Demak, xonada odamlar yo’q.

Algoritm to’gri ishladi✅.

Tuzgan algoritmiz to’gri ishladi. Lekin, tasavvur qiling, xonada 46 ta odam bor. Har birini birma-bir sanab chiqqan bo’larmidingiz? Bunga biroz vaqt ketadi.

Tuzilgan algoritm to’g’ri ishlaydi, ammo **samarador emas**.

Keling, odamlar sonida 1 kishidan emas, har sanaganda 2 kishidan sanaymiz. 2, 4, 6, 8, …

Yangilangan algoritm:

```
N=0
Agar xonada 2 kishini ko'rsak:
    N=N+2
```

Masalaga shart qo’yamiz.

Masala: Xonada 2 kishi bor

?Algoritmni ishga tushiramiz.

**1-qadam**

Odamlar sonini hisoblab boradigan o’zgaruvchini ya’ni N=0 ga tenglashtiramiz.

**2-qadam**

Xonada juftlikni ya’ni 2 kishini ko’rdik va N sonini 2 ga oshiramiz(N+2)

N=N+2⇒

N=0+2⇒

N=2

**3-qadam**

Xonada odam qoldimi? – Yo’q. Demak algoritmni yakunlaymiz

**Javob:** 2 ta

Algoritm ishlashini quyida animatsion ravishda ko’rishingiz mumkin.

<iframe src="https://giphy.com/embed/kFNjbO1QtntIwawC46" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

**Algoritm ishlashi animatsion ko'rinishda**

Yangi tuzgan algoritmiz oldingisidan yaxshigina tez ishladi⏱.

Ushbu algoritmni mukammal deyishga shoshmang. Xonada 3 kishi yoki 5 kishi bo’lsa, algoritm qanday javob qaytararkan ekan.

**Masala**: Xonada 3 kishi bor

Algoritmni ishga tushiramiz.

**1-qadam**

Odamlar sonini hisoblab boradigan o’zgaruvchini ya’ni N=0 ga tenglashtiramiz.

**2-qadam**

Xonada 2 kishi bormi? – Ha. N qiymatini 2 ga oshiramiz(N=N+2).

**3-qadam**

Xonada 2 kishi bormi? – Yo’q. Demak algoritmni yakunlaymiz.

(*Ammo xonada 3 kishi ediku. Bir kishi esdan chiqardik. Chunki, algoritm faqatgina 2 kishini ko’rsa hisoblaydi)

**Javob**: 2 kishi

Xonada 3 kishi, ammo algoritm bizga 2 javobi qaytardi. Demak algoritm o’zimiz hohlagandek, to’g’ri ishlamayapdi❌.

Algoritmda xatolik mavjud. Chunki bizda shart faqatgina juftlikni ya’ni 2 kishi ko’rganda holatini o’ylagandik. Bu algoritm xonada faqatgina juft sondagi odam bo’lsa to’g’ri ishlaydi. Biz sanab bo’lgandan so’ng qolgan bir kishini esdan chiqardik. Demak, algoritmni yana yaxshilaymiz.

```
N=0
Agar xonada 2 kishini ko'rsak:
    N=N+2
Agar xonada 1 kishini ko'rsak:
    N=N+1
```

Yangilangan algoritmda qo’shimcha shart qo’shdik. Ya’ni 2 kishidan sanab bo’lganimizda so’ng xonani tekshiramiz: bir kishi bormi yoki yo’q. Agar bor bo’lsa N qiymatini birga oshir(N=N+1).

Ushbu yozilgan algoritm yuqorida unitib qoldirilgan odamni sanaydi va bizga kutgan natijani olamiz.

Umid qilamanki, siz algoritm haqida umumiy tushincha hosil bo’ldi. Kelasi darslarda esa yanada qiziqarli va foydali ma’lumotni keltirishga harakat qilaman.

Maqolada ishlatilgan rasmlar: manba – [www.youtube.com/watch?v=6hfOvs8pY1k](https://www.youtube.com/watch?v=6hfOvs8pY1k){:target="_blank"}

[Havola](https://nodirbek.uz/2020/07/algoritm-haqida/){:target="_blank"}

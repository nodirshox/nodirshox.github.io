---
layout: post
title: "Dasturlash orqali yuzni tanish texnologiyasi (Face recognition)"
categories: ["face regoncition", "technology", "ai", "programming"]
permalink: /dasturlash-orqali-yuzni-tanish-texnologiyasi-face-recognition
---

Hozirda zamonaviy axborot texnologiyalar juda ko’p qurilmalarda ishlamoqda. Jumladan, kameralar yoki radarlar mashinaning nomerini tez aniqlab oladi. Ushbu maqolada esa qanday qilib yuzni tanish texnologiya ishlatishni ko’rib chiqamiz.

Albatta, biz bu texnologiyani boshidan o’zimiz yozmaymiz. Web sahifani tahrirlash va kompyuterda ishga tushirish uchun bizga **Visual Studio Code** dasturi kerak bo’ladi. Dasturni [code.visualstudio.com](https://code.visualstudio.com/){:target="_blank"} saytidan yuklab olamiz. Dasturni o’rnatib bo’lgach, dasturni ishga tushirib Extensions (CTRL + SHIFT +X) bo’limiga o’tib, “Live server” ni o’rnatib olamiz.

![VS Code](/assets/2019-12-23-face-recognition/vscode.jpg)

**Visual Studio Code**

[Ushbu faylni](https://github.com/justadudewhohacks/face-api.js){:target="_blank"} yuklab olamiz va arxivdan chiqarib olamiz. Visual Studio Code dasturining “File” menyusidan “Open Folder” ni tanlab arxivdan chiqarib olgan papkani ochib olamiz. Endi serverni ishga tushirish uchun ALT + L + O tugmalarini bosib olamiz va web brauzerda ochib beradi. Video tasvirga olishga “Ruhsat berish” (Allow) tugmasini bosamiz va biroz kutamiz. Kompyuter kamerasi orqali ishlab boshlaydi.

![Misol](/assets/2019-12-23-face-recognition/example.jpg)

**Yuzni kvadratga olib kayfiyatning holatini ko’rsatib beradi**

<iframe width="560" height="315" src="https://www.youtube.com/embed/BojAhSgIggk?si=UOOyA-Vlwh5h0p9J" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Real time video**

Endi esa yanada qiziqarli qismga o’tamiz. [Ushbu faylni](https://github.com/WebDevSimplified/Face-Detection-JavaScript){:target="_blank"} yuklab olib Visual Studio Code da ochib olamiz. “rasmlar” degan papkani ichiga kiramiz. Endi Shaxslar uchun papkalar ochamiz. Masalan, ‘Nodirbek Ergashev’ nomli va ichiga 1.jpg nomli 3×4 rasm yoki yuz kesib olingan rasm yuklab qo’yamiz. Huddi shunday qilib boshqa shaxslar rasmlarini yuklab qo’yamiz.

- rasmlar/Nodirbek Ergashev/1.jpg
- rasmlar/Ism Familiya/1.jpg
- rasmlar/Test Uchun/1.jpg

Visual Code Studio da kirib script.js faylini ochib 39-qatordagi kodga o’zimiz qo’shgan shaxslar nomlarini kiritib chiqamiz.

[ ‘Nodirbek Ergashev’, ‘Ism Familiya’, ‘Test Uchun’ ]

Hammasi tayyor va endi serverni yoqamiz[ALT + L + O].

**Rasm yuklashga tayyor!** matni chiqmaguncha kutib turamiz. Matn chiqqandan so’ng, rasm yuklaymiz va Mo’jiza ko’ramiz.

![Misol](/assets/2019-12-23-face-recognition/example2.jpg)

**Obyekt nomi va qanchalik o’xshayotganini ko’rsatuvchi son (0.01~0.99)**

Xulosa, ushbu tayyor Javascript kutubxonadan boshqa dasturlarga biriktirib ishlatsa bo’ladi. Bundan tashqari ushbu kutibxona yosh, jins va videoda real vaqtda ma’lumotlar uzatishi mumkin.

Manba:

- [https://github.com/justadudewhohacks/face-api.js](https://github.com/justadudewhohacks/face-api.js){:target="_blank"}
- [https://github.com/WebDevSimplified/Face-Detection-JavaScript](https://github.com/WebDevSimplified/Face-Detection-JavaScript){:target="_blank"}
- [https://youtu.be/CVClHLwv-4I](https://youtu.be/CVClHLwv-4I){:target="_blank"}

[Havola](https://nodirbek.uz/2019/12/dasturlash-orqali-yuzni-tanish-texnologiyasi-face-recognition/)

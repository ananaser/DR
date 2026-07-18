САЙТ «ЛЕРЕ 35» — КАК ЗАПУСТИТЬ

1. Откройте папку в Sublime Text.
2. Откройте index.html.
3. Для проверки дважды нажмите index.html — он откроется в браузере.

ВАЖНО О СОХРАНЕНИИ:
Без Firebase сайт работает в демо-режиме через localStorage.
В таком режиме отметку о покупке видит только человек на своём устройстве.

Чтобы отметки были общими для всех гостей:

1. Откройте https://console.firebase.google.com/
2. Создайте новый проект.
3. Откройте Build → Firestore Database → Create database.
4. Добавьте Web App в настройках проекта.
5. Скопируйте firebaseConfig.
6. Вставьте значения в объект firebaseConfig внутри index.html.

Для теста можно установить Firestore Rules:

rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /giftReservations/{giftId} {
      allow read: if true;
      allow create: if
        request.resource.data.reserved == true;
      allow update, delete: if false;
    }
  }
}

Такие правила позволяют:
- всем видеть выбранные подарки;
- отметить ещё свободный подарок как купленный;
- не перезаписывать и не удалять чужой выбор.

ПУБЛИКАЦИЯ:
Самый простой вариант — Netlify Drop:
1. Откройте https://app.netlify.com/drop
2. Перетащите туда всю папку lera_35_wishlist.
3. Получите публичную ссылку и отправьте гостям.

КАРТИНКИ:
Сейчас используются аккуратные локальные иллюстрации:
- yacht.svg
- spa.svg
- airbnb.svg
- sunglasses.svg

Их можно заменить настоящими фотографиями.
Положите новые файлы в эту же папку и измените поле image в массиве gifts.

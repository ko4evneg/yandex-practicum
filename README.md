## Уровень 1. Проектирование
1. В проекте используются shared компоненты, типа Header, Footer.
2. Проект использует один фреймворк
3. Проект рассчитан на малое количество юзеров

Исходя из этих пунктов, выбран подход Module Federation так как соответственно:
1. обеспечивает более простую работу с shared компонентами
2. использование разных фреймворков не требуется
3. не требуется высокая производительность проекта

Однако, если допустить, что в бизнес требованиях мы видим, что планируется веб-фронтенд для инстаграма, 
то выбор будет в пользу Single SPA - из-за ожидаемой большой нагрузки, необходимости разделения на 
команды ввиду размера штата, необходимости использования разных фреймворков (для показа видео - нужно
производительное решение, для платежей - надежное и т. д.) и увеличения надежности при отказе одного из
компонентов (будет достигаться большей изоляцией компонентов по сравнению с MF).

## Уровень 2. Планирование изменений

В приложение выделено 5 микрофронтендов:
1. Host - микрофронтенд, содержащий общие компоненты и отвечающий за координацию вызовов остальных МФ.
2. Auth - МФ, отвечающий за аутентификацию и регистрацию юзеров
3. Cards - МФ, отвечающий за работу с фотографиями
4. Places - МФ, отвечаюий за работу с местами (на раннем этапе можно объединить с МФ 3)
5. Profiles - МФ, отвечающий за работу с профилями пользователя (на раннем этапе можно объединить с МФ 2)

Микрофронтенды разбиты принципом вертикальной нарезки - так как границы доменных областей хорошо видны, а 
также есть наличие shared компонентов и отсутствует необходимость в автономности команд.
    

Структура:
```
microfrontend
    /auth/src
        /components
            Login.js
            Register.js
            CurrentUserContext
        /utils
            auth.js
        /blocks
            auth-form/
            login/
    /cards/src
        /components
            Card.js
            ImagePopup.js
        /blocks
            card/
    /host/src
        /components
            App.js
            Footer.js
            Header.js
            InfoTooltip.js
            Main.js
            PopupWithForm.js
            ProtectedRoute.js
            index.js
            serviceWorker.js
            setupTests.js
        /utils
            api.js
        /blocks
            footer/
            header/
            page/
            content/
            popup/
    /places/src
        /components
            AddPlacePopup.js
        /blocks
            places/
    /profiles/src
        /components
            EditAvatarPopup.js
        /blocks
            profile/
```

# WP-формат (Gutenberg + власні <style>) - тільки для new/ і для edit/, якщо старий сайт у WP-блоках

Референс коду: `new/example.txt` (зразок формату, не джерело фактів).

## Файли
- Папка на бренд: `new/output/<Brand>/`, 1-3 файли `<slug>-template1..3.html`; якщо клієнт дав назву сайту - файл за цим слагом і його палітра (без палітри - тимчасова).
- 3 шаблони одного бренду йдуть на РІЗНІ сайти: різний дизайн таблиць, іконок, декору, розміщення CTA-банерів. Між брендами теж не повторювати комбінацію елементів і місця банерів.
- `[seo_content]` рівно перед першим `<h2>` (якщо вимагає тема сайту).

## Кольори і захист від теми (WP-тема перебиває наївний CSS)
1. Усі `color`/`background` у власних `<style>` з `!important`; колір задавати явно на кожному текстовому елементі (`td`, `strong`, `p`, `li`), не покладатись на успадкування.
2. Контраст: темний фон -> майже білий текст (#F5F0E8/#FFF), світлий/золотий/акцентний фон -> майже чорний (#0d0c0b). Акцент лише для бордерів/іконок/лейблів. Звіряти `color` з реальним фоном найближчого контейнера.
3. Захисний блок для `<a>` і правил з реальним `color:`:
   `-webkit-text-fill-color:<той самий колір> !important; background-image:none !important; -webkit-background-clip:initial !important; background-clip:initial !important; text-shadow:none !important;`
   Для CTA-кнопок і "Official Website" дублювати inline `style=""` на `<a>`.
4. НЕ додавати `-webkit-text-fill-color` у правила, що задають лише фон (зебра-рядки, :hover) - текст стане невидимим.
5. Кожен `<th>` - inline `style` (background + color + fill-color + захисний блок), включно з colspan. `thead`, `thead tr`, `th` - background на всіх трьох рівнях.
6. H3 на сторінці (поза кольоровою коробкою): тільки `border-left:3px solid <акцент>; padding-left:12px; margin 28px/12px`, без форсованого кольору і без "чіпа". Виняток - H3 у FAQ `<summary>` (форсувати колір, скинути `background:none`, `border:none`).
7. `list-style: none/decimal !important` явно на `<ul>/<ol>/<li>`.
8. Перевірка: зібрати локальний прев'ю (білий фон, темні дефолтні strong/p/h3) і глянути скріншотом: перша таблиця, H3, FAQ відкритий/закритий.

## CTA-банер
1-2 на сторінку: `<div class="XX-cta-banner"><p class="XX-cta-text">...</p><a href="/go/" class="XX-cta-button">Claim Your Bonus</a></div>`. Справжній `<a href="/go/">`, стиль кнопки за правилами кольору вище. Місце міняти між брендами.

## Quick Facts
Завжди справжня `<table><thead><tr><th>` з іконкою (emoji/бейдж) у кожному рядку, у всіх шаблонах. Рядок Official Website - `<a href="/go/">`, інлайн-захист.

## Перед здачею (скрипт)
- Баланс `<!-- wp:X -->` / `<!-- /wp:X -->` (heading, paragraph, html, list, list-item) і HTML-тегів (div, style, table, thead, tbody, tr, td, th, details, ol, ul, li). Непарний wp:html коментар ламає всю сторінку в сирий код. Найчастіше - у довгих fact-cards/spec-list блоках.
- Кожне CSS-правило з `-webkit-text-fill-color` має мати у собі й звичайний `color:`.
- Non-ASCII у прозі (емоджі-іконки лише в дизайні).

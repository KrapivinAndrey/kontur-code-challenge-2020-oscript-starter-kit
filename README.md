# kontur-code-challenge-2020-oscript-starter-kit

Стартовый проект для участия https://tech.kontur.ru/code-challenge

## Быстрый старт

```bsl
#Использовать json

Процедура Игра()

    Консоль = Новый Консоль();
    Json = Новый ПарсерJSON();

    // Фаза Draft https://codechallenge.testkontur.ru/rules.html#%D0%A4%D0%B0%D0%B7%D0%B0-Draft
    Консоль.ПрочитатьСтроку();
    Консоль.ВывестиСтроку("{""Message"": ""draft debug msg""}");

    Пока Истина Цикл

        // Фаза Battle https://codechallenge.testkontur.ru/rules.html#%D0%A4%D0%B0%D0%B7%D0%B0-Battle
        Ход = Json.ПрочитатьJSON(Консоль.ПрочитатьСтроку());
        Команды = Новый Массив;
        Для Каждого Корабль Из Ход["My"] Цикл

            // Battle-Input https://codechallenge.testkontur.ru/rules.html#Input1
            Противник = Ход["Opponent"][0]["Position"];
            Двигаться = Новый Структура("Id, Target", Корабль["Id"], Противник);
            Атаковать = Новый Структура("Id, Name, Target", Корабль["Id"], "big_blaster", Противник);

            // Battle-Output https://codechallenge.testkontur.ru/rules.html#Output1
            Команды.Добавить(Новый Структура("Command, Parameters", "MOVE", Двигаться));
            Команды.Добавить(Новый Структура("Command, Parameters", "ATTACK", Атаковать));

        КонецЦикла;

        Действие = Новый Структура("UserCommands, Message", Команды, "battle debug msg");
        Консоль.ВывестиСтроку(Json.ЗаписатьJSON(Действие, Ложь));

    КонецЦикла;

КонецПроцедуры

Игра();

```

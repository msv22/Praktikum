{
  "title": "Python с нуля",
  "description": "Демонстрационный курс: все типы шагов, обязательное ДЗ, авто-зачёт.",
  "version": "1.0",
  "modules": [
    {
      "title": "Старт",
      "lessons": [
        {
          "title": "Переменные и типы",
          "steps": [
            { "type": "text", "content": "### Переменная — имя для значения\n\n```python\nage = 25\nname = \"Аня\"\nprice = 199.9\n```\n\nОсновные типы: `int`, `float`, `str`, `bool`. Тип узнаём через `type(x)`." },
            { "type": "quiz", "question": "Какой тип у значения `3.0`?", "options": ["int","float","str"], "correct": [1], "explanation": "Точка делает число float." },
            { "type": "input", "question": "Чему равно `int(\"7\") + 3`? (числом)", "answer": "10", "match": "number" }
          ],
          "homework": [
            { "type": "input", "question": "Функция, возвращающая длину строки? (только имя)", "answer": "len", "match": "exact" }
          ]
        }
      ]
    }
  ]
}

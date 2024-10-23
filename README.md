# Mathematic-theory-of-risks

#Lab 1

<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Рішення про пікнік</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }

        h2 {
            text-align: center;
        }

        .form-container {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
        }

        .form-container input {
            margin-right: 10px;
            padding: 5px;
        }

        canvas {
            display: block;
            margin: 0 auto;
        }

        #decision {
            text-align: center;
            margin-top: 20px;
            font-size: 18px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <h2>Рішення про пікнік: Ліс чи Місто?</h2>

    <div class="form-container">
        <div>
            <label for="probability">Ймовірність дощу (від 0 до 1):</label>
            <input type="number" id="probability" min="0" max="1" step="0.1" value="0.5">
        </div>
        <button onclick="updateGraph()">Оновити графік</button>
    </div>

    <canvas id="picnicChart" width="600" height="400"></canvas>

    <div id="decision"></div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // Вихідні корисності для лісу та міста
        const forestUtilities = {
            'дуже погано': 0,
            'погано': 3,
            'посередньо': 5,
            'чудово': 8
        };

        const cityUtilities = {
            'дуже погано': 1,
            'погано': 4,
            'посередньо': 6,
            'чудово': 7
        };

        // Функція для обчислення корисності
        function calculateUtility(probability, utilityMap) {
            return utilityMap['дуже погано'] * (1 - probability) + utilityMap['чудово'] * probability;
        }

        // Створення початкового графіка
        const ctx = document.getElementById('picnicChart').getContext('2d');
        const picnicChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: [0.0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0],
                datasets: [
                    {
                        label: 'Ліс',
                        data: [],
                        borderColor: 'purple',
                        fill: false
                    },
                    {
                        label: 'Місто',
                        data: [],
                        borderColor: 'blue',
                        fill: false
                    }
                ]
            },
            options: {
                scales: {
                    x: {
                        title: {
                            display: true,
                            text: 'Ймовірність дощу'
                        }
                    },
                    y: {
                        title: {
                            display: true,
                            text: 'Корисність'
                        },
                        suggestedMin: 0,
                        suggestedMax: 10
                    }
                }
            }
        });

        // Оновлення даних графіка та рішення
        function updateGraph() {
            const probability = parseFloat(document.getElementById('probability').value);

            let forestData = [];
            let cityData = [];

            // Обчислення даних для графіка
            for (let i = 0; i <= 1; i += 0.1) {
                forestData.push(calculateUtility(i, forestUtilities));
                cityData.push(calculateUtility(i, cityUtilities));
            }

            // Оновлення даних на графіку
            picnicChart.data.datasets[0].data = forestData;
            picnicChart.data.datasets[1].data = cityData;
            picnicChart.update();

            // Обчислення рішення на основі вибраної ймовірності
            const forestUtility = calculateUtility(probability, forestUtilities);
            const cityUtility = calculateUtility(probability, cityUtilities);
            const decisionElement = document.getElementById('decision');

            if (forestUtility > cityUtility) {
                decisionElement.textContent = 'Краще піти до лісу!';
            } else if (forestUtility < cityUtility) {
                decisionElement.textContent = 'Краще залишитися в місті!';
            } else {
                decisionElement.textContent = 'Обидва варіанти однаково добрі!';
            }
        }

        // Початкове відображення графіка
        updateGraph();
    </script>

</body>
</html>

Result: 
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/1.png)
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/2.png)
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/4.png)

#Lab 2

#Завдання 8:  Орендне підприємство, яке виробляє м’які куточки в великому асортименті, має можливість укласти дві різні угоди: першу угоду з фірмою в цьому ж місті, другу – з фірмою іншого міста, але з більш вигідними поставками. Можливі два варіанти прибутку при виборі першої фірми: 9000 гривень, якщо фірма буде мати змогу вкласти нову угоду, 7000 гривень , якщо це буде одинична поставка. При виборі другої фірми: 13000 гривень та 7500 гривень з урахуванням поставок. Результати та відповідні їм ймовірності наведені в таблиці. Вибрати найменш ризиковане рішення та оцінити величину ризику.
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.2.png)


def calculate_expected_profit(probabilities, profits):
    return sum(p * profit for p, profit in zip(probabilities, profits))

def main_decision_task():
    # Дані з таблиці
    probabilities_1 = [0.7, 0.3]
    profits_1 = [9000, 7000]

    probabilities_2 = [0.4, 0.6]
    profits_2 = [13000, 7500]

    # Обчислення очікуваного прибутку
    expected_profit_1 = calculate_expected_profit(probabilities_1, profits_1)
    expected_profit_2 = calculate_expected_profit(probabilities_2, profits_2)

    print(f"Очікуваний прибуток (Фірма 1): {expected_profit_1} грн")
    print(f"Очікуваний прибуток (Фірма 2): {expected_profit_2} грн")

    if expected_profit_1 > expected_profit_2:
        print("Рекомендується вибрати Фірму 1")
    else:
        print("Рекомендується вибрати Фірму 2")

if __name__ == "__main__":
    main_decision_task()

def calculate_expected_profit(probabilities, profits):
    return sum(p * profit for p, profit in zip(probabilities, profits))

def main_decision_task():
    # Дані з таблиці
    probabilities_1 = [0.7, 0.3]
    profits_1 = [9000, 7000]

    probabilities_2 = [0.4, 0.6]
    profits_2 = [13000, 7500]

    # Обчислення очікуваного прибутку
    expected_profit_1 = calculate_expected_profit(probabilities_1, profits_1)
    expected_profit_2 = calculate_expected_profit(probabilities_2, profits_2)

    print(f"Очікуваний прибуток (Фірма 1): {expected_profit_1} грн")
    print(f"Очікуваний прибуток (Фірма 2): {expected_profit_2} грн")

    if expected_profit_1 > expected_profit_2:
        print("Рекомендується вибрати Фірму 1")
    else:
        print("Рекомендується вибрати Фірму 2")

if __name__ == "__main__":
    main_decision_task()

Result:
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Без%20имени.png)

#Lab.3

#Завдання 8: Користуючись концепцією корисності за Нейманом, порівняйте ефективність рішень, поданих у таблиці (прибуток у десятках тисяч доларів), якщо відомо, що функція корисності задається формулою: 
U (x) = (x + 5) ^ 2 / 15
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.3%20(умова).png)

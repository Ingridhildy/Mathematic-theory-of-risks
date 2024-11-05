# Mathematic-theory-of-risks

# Lab 1

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
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.1(res.1).png)
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.1(res.2).png)
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.1(res.3).png)

# Lab 2

#Завдання 8:  Орендне підприємство, яке виробляє м’які куточки в великому асортименті, має можливість укласти дві різні угоди: першу угоду з фірмою в цьому ж місті, другу – з фірмою іншого міста, але з більш вигідними поставками. Можливі два варіанти прибутку при виборі першої фірми: 9000 гривень, якщо фірма буде мати змогу вкласти нову угоду, 7000 гривень , якщо це буде одинична поставка. При виборі другої фірми: 13000 гривень та 7500 гривень з урахуванням поставок. Результати та відповідні їм ймовірності наведені в таблиці. Вибрати найменш ризиковане рішення та оцінити величину ризику.
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.2%20(умова).png)


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
![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.2%20(result).png)

# Lab.3

#Завдання 8: Користуючись концепцією корисності за Нейманом, порівняйте ефективність рішень, поданих у таблиці (прибуток у десятках тисяч доларів), якщо відомо, що функція корисності задається формулою: 
U (x) = (x + 5) ^ 2 / 15

![Image alt](https://github.com/Ingridhildy/Mathematic-theory-of-risks/blob/main/Lab.3%20(умова).png)

#Дано
profits = {
    "I": [10, -5, -5],
    "II": [-5, -5, 10],
    "III": [1.5, 1.5, 0],
    "IV": [0, 0, 0]
}
probabilities = [0.5, 0.1, 0.4]

#Функція обчислення корисності
def utility(x):
    return ((x + 5) ** 2) / 15

#Обчислення очікуваної корисності для кожного рішення
expected_utilities = {}
for decision, profits_list in profits.items():
    expected_utility = sum(prob * utility(profit) for prob, profit in zip(probabilities, profits_list))
    expected_utilities[decision] = expected_utility

#Виведення результатів
for decision, expected_utility in expected_utilities.items():
    print(f"Очікувана корисність для рішення {decision}: {expected_utility:.2f}")

Result:
![image](https://github.com/user-attachments/assets/e479ec14-dcef-4eec-bd8a-7aa994715fec)



# Lab 4

#Завдання 8: Акції виду А1, А2, А3 мають, відповідно, сподівані норми прибутку
10%, 20% та 50%, середньоквадратичні відхилення 2%, 10% та 20%, коефіцієнти кореляції p12 = 0, p13 = 0 та p23 = – 0,6. Необхідно:
а) визначити оптимальну структуру ПЦП щодо збереження капіталу;
б) визначити оптимальну структуру ПЦП щодо збільшення приросту капіталу при m(c) = 30%;
в) визначити оптимальну структуру ПЦП щодо максимального збільшення приросту капіталу при σ(с) = 15%;
г) для всіх отриманих ПЦП обчислити сподівану норму прибутку та величину ризику.

import numpy as np
from scipy.optimize import minimize

#Вхідні дані
expected_returns = np.array([0.10, 0.20, 0.50])  # Сподівані норми прибутку
std_devs = np.array([0.02, 0.10, 0.20])          # Середньоквадратичні відхилення
correlation_matrix = np.array([
    [1, 0, 0],
    [0, 1, -0.6],
    [0, -0.6, 1]
])

#Розрахунок ковариаційної матриці
cov_matrix = np.diag(std_devs) @ correlation_matrix @ np.diag(std_devs)

#Функція для розрахунку ризику портфеля
def portfolio_risk(weights):
    return np.sqrt(weights @ cov_matrix @ weights)

#Функція для розрахунку сподіваної норми прибутку портфеля
def portfolio_return(weights):
    return weights @ expected_returns

#Обмеження: сума ваг дорівнює 1
constraints = ({'type': 'eq', 'fun': lambda weights: np.sum(weights) - 1})

#Обмеження ваг: 0 <= weight <= 1
bounds = [(0, 1) for _ in range(3)]

#Оптимізація для мінімізації ризику (а)
weights_0 = np.array([1/3, 1/3, 1/3])  # Початкове припущення
result_risk_min = minimize(portfolio_risk, weights_0, bounds=bounds, constraints=constraints)
optimal_weights_risk_min = result_risk_min.x

#Оптимізація для максимізації прибутку при m(c) = 30% (б)
target_return = 0.30
constraints_return = [
    {'type': 'eq', 'fun': lambda weights: np.sum(weights) - 1},
    {'type': 'eq', 'fun': lambda weights: portfolio_return(weights) - target_return}
]
result_return_max = minimize(portfolio_risk, weights_0, bounds=bounds, constraints=constraints_return)
optimal_weights_return_max = result_return_max.x

#Оптимізація для максимального приросту при σ(с) = 15% (в)
target_risk = 0.15
constraints_risk = [
    {'type': 'eq', 'fun': lambda weights: np.sum(weights) - 1},
    {'type': 'ineq', 'fun': lambda weights: target_risk - portfolio_risk(weights)}
]
result_risk_target = minimize(lambda weights: -portfolio_return(weights), weights_0, bounds=bounds, constraints=constraints_risk)
optimal_weights_risk_target = result_risk_target.x

#Розрахунок отриманих сподіваних норм прибутку і ризиків
optimal_returns = [
    portfolio_return(optimal_weights_risk_min),
    portfolio_return(optimal_weights_return_max),
    portfolio_return(optimal_weights_risk_target)
]
optimal_risks = [
    portfolio_risk(optimal_weights_risk_min),
    portfolio_risk(optimal_weights_return_max),
    portfolio_risk(optimal_weights_risk_target)
]

print("Оптимальні ваги для мінімізації ризику:", optimal_weights_risk_min);
print("Оптимальні ваги для приросту капіталу при m(c) = 30%:", optimal_weights_return_max);
print("Оптимальні ваги для максимального приросту при σ(с) = 15%:", optimal_weights_risk_target);
print("Сподівані норми прибутку:", optimal_returns);
print("Ризики:", optimal_risks);

Result:
![image](https://github.com/user-attachments/assets/edd6f179-177a-406e-ac4d-734178bf4019)


# Lab 5

#Завдання 8:  Вибір фірми, що здатна стати партнером в сумісному підприємництві для машинобудівного підприємства, пов'язаний в першу чергу, з визначенням технічних можливостей співробітництва. Відсутність у вітчизняного підприємства значних фінансових резервів у ВКВ зумовлює необхідність залучення зарубіжних партнерів, що є метою створення виробництва, яке стане конкурентноздатним на зовнішньому ринку, або такого, що замінює імпорт за умови повної валютної самоокупності. Керівництво підприємства повинне зробити вибір однієї з пропозицій зарубіжних фірм: x1 - фірма-партнер пропонує все основне технологічне обладнання (станки, преси тощо); x2 - компанія надає право на промислову власність (торгову марку і ліцензії); x3 - фірма передає інструменти, додаткове обладнання, "ноу-хау"; x4 - компанія приймає участь тільки в наданні грошових засобів в ВКВ.
На продукцію підприємства може бути: великий попит; середній попит; низький попит.
Виходячи з цього, керівництву підприємства була надана матриця прибутків (тис. дол.):
F = (  45    32    16
       15    8     10
       20    18    14
       30    23    7  )
Керівництво підприємства цікавить така пропозиція зарубіжних фірм, яка дає можливість отримати як максимальний сподіваний прибуток, так і мати мінімальний ризик. Знайти компромісне рішення, скориставшись критерієм Ходжеса-Лемана та модифікованими критеріями при λ ∈  [0; 1].


import numpy as np

#Матриця прибутків (тис. дол.)
F = np.array([
    [45, 32, 16],
    [15, 8, 10],
    [20, 18, 14],
    [30, 23, 7]
])

#Сподівані прибутки і ризики для кожної фірми
expected_profits = np.mean(F, axis=1)
risks = np.std(F, axis=1)

#Функція критерію Ходжеса-Лемана
def hodges_lehmann_criterion(lmbda):
    return (1 - lmbda) * expected_profits - lmbda * risks

#Пошук найкращих рішень при різних λ
lambda_values = np.linspace(0, 1, 11)
best_firm_by_lambda = [np.argmax(hodges_lehmann_criterion(lmbda)) for lmbda in lambda_values]

print("Найкращі фірми при різних λ:", best_firm_by_lambda)

Result:

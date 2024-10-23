# Mathematic-theory-of-risks

#Lab 1


#Lab 2

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
![Image alt](https://github.com/{username}/{repository}/raw/{branch}/{path}/image.png)

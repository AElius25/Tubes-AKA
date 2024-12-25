import random
import time
import matplotlib.pyplot as plt
from prettytable import PrettyTable

# Definisikan rarity item
class ItemRarity:
    Common = "Common"
    Uncommon = "Uncommon"
    Rare = "Rare"
    Legendary = "Legendary"

# Iteratif
def gacha_iterative(max_trials):
    probability_legendary = 0.005  # 0.5% chance to get Legendary
    probability_rare = 0.05        # 5% chance to get Rare
    probability_uncommon = 0.2     # 20% chance to get Uncommon

    for trials in range(1, max_trials + 1):
        rand_value = random.random()
        if rand_value < probability_legendary:
            return ItemRarity.Legendary, trials
        elif rand_value < probability_legendary + probability_rare:
            return ItemRarity.Rare, trials
        elif rand_value < probability_legendary + probability_rare + probability_uncommon:
            return ItemRarity.Uncommon, trials
    return ItemRarity.Common, max_trials

# Rekursif
def gacha_recursive(trials, max_trials):
    probability_legendary = 0.005  # 0.5% chance to get Legendary
    probability_rare = 0.05        # 5% chance to get Rare
    probability_uncommon = 0.2     # 20% chance to get Uncommon

    if trials >= max_trials:
        return ItemRarity.Common, max_trials

    rand_value = random.random()
    if rand_value < probability_legendary:
        return ItemRarity.Legendary, trials + 1
    elif rand_value < probability_legendary + probability_rare:
        return ItemRarity.Rare, trials + 1
    elif rand_value < probability_legendary + probability_rare + probability_uncommon:
        return ItemRarity.Uncommon, trials + 1

    return gacha_recursive(trials + 1, max_trials)

# Grafik untuk menyimpan data
trial_values = []
recursive_times = []
iterative_times = []
iterative_pulls = []
recursive_pulls = []

# Fungsi untuk memperbarui grafik
def update_graph():
    plt.figure(figsize=(8, 6))
    plt.plot(trial_values, recursive_times, label='Recursive Time', marker='o', linestyle='-')
    plt.plot(trial_values, iterative_times, label='Iterative Time', marker='o', linestyle='-')
    plt.title('Performance Comparison: Recursive vs Iterative (Gacha)')
    plt.xlabel('Max Trials')
    plt.ylabel('Execution Time (seconds)')
    plt.legend()
    plt.grid(True)
    plt.show()

# Fungsi untuk mencetak tabel waktu eksekusi
def print_execution_table():
    table = PrettyTable()
    table.field_names = ["Max Trials", "Recursive Time (s)", "Iterative Time (s)", 
                         "Recursive Pulls", "Iterative Pulls"]
    min_len = min(len(trial_values), len(recursive_times), len(iterative_times),
                  len(iterative_pulls), len(recursive_pulls))
    for i in range(min_len):
        table.add_row([trial_values[i], recursive_times[i], iterative_times[i], 
                       recursive_pulls[i], iterative_pulls[i]])
    print(table)

# Program utama
while True:
    try:
        max_trials = int(input("Masukkan jumlah maksimal percobaan (atau ketik -1 untuk keluar): "))
        if max_trials == -1:
            print("Program selesai. Terima kasih!")
            break
        if max_trials <= 0:
            print("Masukkan jumlah percobaan yang positif!")
            continue

        trial_values.append(max_trials)

        # Ukur waktu eksekusi algoritma iteratif
        start_time = time.time()
        _, iterative_pull_count = gacha_iterative(max_trials)
        iterative_times.append(time.time() - start_time)
        iterative_pulls.append(iterative_pull_count)

        # Ukur waktu eksekusi algoritma rekursif
        start_time = time.time()
        _, recursive_pull_count = gacha_recursive(0, max_trials)
        recursive_times.append(time.time() - start_time)
        recursive_pulls.append(recursive_pull_count)

        # Cetak tabel waktu eksekusi
        print_execution_table()

        # Perbarui grafik
        update_graph()

    except ValueError:
        print("Masukkan nilai maksimal percobaan yang valid!")

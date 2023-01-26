# VendingMachine

class Item:

    def __init__(self, name, price):
        self.name = name
        self.price = price

class VendingMachine:

    def __init__(self):

        self.items = [
            Item("Καφές", 1.50),
            Item("Καφές με γάλα", 1.80),
            Item("Σοκολάτα", 2.10),
            Item("Σοκολάτα με γάλα", 2.40),
            Item("Έξοδος", 0)
        ]

        self.money_inserted = 0.00

    def display_items(self):
        for code, item in enumerate(self.items, start=1):
            print(f"{code}. {item.name} {item.price:.2f}€")

    def insert_money(self, money):
        coins = [0.10, 0.20, 0.50, 1, 2, 5, 10]
        if money <= 0.00:
            raise ValueError
        if money in coins:
            self.money_inserted += money
        else:
            print("ΣΦΑΛΜΑ!: εισαγωγή μη έγκυρου ποσού. \nΠαρακαλώ εισάγετε ενα έγκυρο ποσό: 0.10/0.20/0.50/1/2/5/10")

def main():

    vending_machine = VendingMachine()
    vending_machine.display_items()

    while True:
        try:
            choice = int(input("Παρακαλώ εισάγετε την επιλογή σας (0-4) ή 0 για έξοδο:"))
        except ValueError:
            continue
        if choice in range(1, len(vending_machine.items)+1):
            break
    item = vending_machine.items[choice-1]
    if choice == 5:
        return print("Αντίο σας!")

    print(f"Επιλέξατε :{item.name} \nΠρέπει να εισάγετε {item.price:.2f}€:")
    while vending_machine.money_inserted < item.price:
        print(f"Έχετε τοποθετήσει {vending_machine.money_inserted:.2f}€ στο μηχάνημα μέχρι στιγμής.")
        while True:
            try:
                money_to_insert = float(input("Εισαγάγετε το χρηματικό ποσό που θέλετε: "))
                vending_machine.insert_money(money_to_insert)
            except ValueError:
                continue
            else:
                break
    refund = vending_machine.money_inserted - item.price
    print(f"Παρακαλώ πάρτε: {item.name}.")
    print(f"Τα ρέστα σας είναι: {refund:.2f}€.")

    two = refund // 2
    m_two = refund % 2
    one = m_two // 1
    m_one = m_two % 1
    fifty = m_one // 0.50
    m_fifty = m_one % 0.50
    twenty = m_fifty //0.20
    m_twenty = fifty % 0.20
    ten = m_twenty // 0.10


    print("Παρακαλώ πάρτε: ")
    print(f"Δίευρα: {two}\nΜονόευρα: {one}\nΠενηντάλεπτα: {fifty}\nΕικοσάλεπτα :{twenty} \nΔεκάλεπτα:{ten}")


    return 0

if __name__ == "__main__":
    import sys
    sys.exit(main())

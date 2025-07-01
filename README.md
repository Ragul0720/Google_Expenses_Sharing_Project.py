import matplotlib.pyplot as plt

class ExpenseSharing:
    def __init__(self, friends):
        self.friends = friends
        self.balances = {friend: 0 for friend in friends}
        self.transactions = []  # to keep record of expenses

    def add_expense(self, payer, amount, participants, weights=None):
        # Handle weighted contributions
        if weights:
            total_weight = sum(weights)
            splits = [amount * (w / total_weight) for w in weights]
        else:
            splits = [amount / len(participants)] * len(participants)

        # Update balances
        for i, participant in enumerate(participants):
            self.balances[participant] -= splits[i]
        self.balances[payer] += amount

        # Record the transaction for audit / later insights
        self.transactions.append({
            "payer": payer,
            "amount": amount,
            "participants": participants,
            "splits": splits
        })

    def calculate_settlement(self):
        creditors = []
        debtors = []

        for friend, balance in self.balances.items():
            if balance > 0:
                creditors.append((friend, balance))
            elif balance < 0:
                debtors.append((friend, -balance))  # positive debt

        while debtors and creditors:
            debtor, debt_amount = debtors.pop()
            creditor, credit_amount = creditors.pop()

            payment = min(debt_amount, credit_amount)
            print(f"{debtor} owes {creditor}: Rs. {payment:.2f}")

            if debt_amount > payment:
                debtors.append((debtor, debt_amount - payment))
            if credit_amount > payment:
                creditors.append((creditor, credit_amount - payment))

    def print_final_balances(self):
        print("\n--- Final Balance Sheet ---")
        for friend, balance in self.balances.items():
            print(f"{friend}: Rs. {balance:.2f}")

    def visualize_balances(self):
        friends = list(self.balances.keys())
        balances = list(self.balances.values())

        plt.figure(figsize=(8, 5))
        plt.bar(friends, balances, color='skyblue')
        plt.axhline(0, color='gray', linestyle='--')
        plt.title("Final Balances of Friends")
        plt.xlabel("Friend")
        plt.ylabel("Balance (Rs.)")
        plt.tight_layout()
        plt.show()

if __name__ == "__main__":
    friends = input("Enter the names of friends, separated by commas: ").split(",")
    friends = [friend.strip() for friend in friends]

    expense_sharing = ExpenseSharing(friends)

    while True:
        payer = input("Enter the name of the person who paid (or 'done' to finish): ")
        if payer.lower() == "done":
            break

        amount = float(input("Enter the amount paid (negative for refunds): "))

        participants = input("Enter the names of participants, separated by commas: ").split(",")
        participants = [participant.strip() for participant in participants]

        use_weights = input("Do you want to enter weights for uneven split? (yes/no): ").lower()
        if use_weights == "yes":
            weights = list(map(float, input("Enter weights separated by commas (matching participants order): ").split(",")))
            expense_sharing.add_expense(payer, amount, participants, weights)
        else:
            expense_sharing.add_expense(payer, amount, participants)

    print("\n--- Settlement Summary ---")
    expense_sharing.calculate_settlement()
    expense_sharing.print_final_balances()
    expense_sharing.visualize_balances()

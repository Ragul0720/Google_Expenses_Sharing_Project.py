# 💸 Expense Sharing System (Google Pay-Inspired)

A Python-based expense sharing tool inspired by Google Pay group expenses. This project helps users fairly split expenses among friends and calculate who owes whom. It supports equal and weighted splits, refunds, and visualizes balances using `matplotlib`.

---

## 📌 Features

- ✅ Equal and weighted (custom ratio) expense splitting
- 💰 Handles refunds (negative expenses)
- 🔄 Real-time balance tracking and debt settlements
- 📊 Final balance visualization with `matplotlib`
- 🧮 Fairness logic to minimize total number of transactions
- 📝 CLI-based input and tracking of all transactions

---

## 🛠 Tech Stack

- Python 3.x  
- Pandas (for tracking and storing transactions)  
- Matplotlib (for data visualization)

---

## 🧪 How It Works

1. Users are prompted to enter names of friends involved.
2. As expenses are added:
   - The system splits them equally or based on weights.
   - Balances are updated in real time.
3. When finished, the system:
   - Calculates settlements (who owes whom)
   - Displays a final balance sheet
   - Plots a bar chart of all balances

---

## 🚀 Example Usage

```bash
Enter the names of friends, separated by commas: Alice,Bob,Charlie

Enter the name of the person who paid (or 'done' to finish): Alice
Enter the amount paid (negative for refunds): 300
Enter the names of participants, separated by commas: Alice,Bob,Charlie
Do you want to enter weights for uneven split? (yes/no): no

... (enter more expenses)

--- Settlement Summary ---
Bob owes Alice: Rs. 100.00
Charlie owes Alice: Rs. 100.00

--- Final Balance Sheet ---
Alice: Rs. 200.00
Bob: Rs. -100.00
Charlie: Rs. -100.00


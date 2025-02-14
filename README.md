   📘  **Smart Financial Management System** 

📍**FAST National University of Computer and Emerging Sciences **(FAST-NUCES)**, Islamabad**

👨‍🏫 **Instructor:** **Dr. Usama Arshad (Assistant Professor, FSM)**

🎓 **Program:** **BS Financial Technology** **(BSFT)**

📅 **Semester:** **Spring 2025**


 ## **🟢 Part 1: Loan Eligibility & Interest Rate Calculation [4 marks]**  

📌 **Requirement:**  
SecureBank only approves loans if the **customer meets all eligibility criteria**. The system should:  
✔ **Check if the customer is employed.**  
✔ **Verify if the income is at least PKR 50,000.**  
✔ **Check credit score:**  
   - **750+ → 5% Interest Rate**  
   - **650 - 749 → 8% Interest Rate**  
   - **Below 650 → Loan Rejected**  
✔ **If the applicant is unemployed, the loan is rejected immediately.**  

### **Implementation Steps:**  
🔹 **Step 1:** Structure the `if-elif-else` statements for this logic.  
🔹 **Step 2:** Implement a Python program using **ipywidgets** for interactive user input (income, credit score, employment status) to decide whether the loan is approved or rejected.

---
       def check_loan_eligibility():
    employed = input("Are you employed? (yes/no): ").lower()
    income = float(input("What is your monthly income in PKR? "))
    credit_score = int(input("What is your credit score? "))

    if employed == "no":
        print("Loan Rejected: You must be employed to qualify for a loan.")
        return

    if income < 50000:
        print("Loan Rejected: Your income must be at least PKR 50,000 to qualify for a loan.")
        return

    if credit_score >= 750:
        interest_rate = 5
    elif credit_score >= 650 and credit_score <= 749:
        interest_rate = 8
    else:
        print("Loan Rejected: Your credit score is too low.")
        return

    print("Loan Approved!")
    print(f"Your interest rate is: {interest_rate}%")

    check_loan_eligibility()

## **🟢 Part 2: Investment Risk Assessment [4 marks]**  

📌 **Requirement:**  
SecureBank offers **investment analysis services**. The system should evaluate a **portfolio of stocks** and classify the risk level based on stock returns:  
✔ If **any stock has a negative return**, the portfolio is **High Risk**.  
✔ If **all stocks have positive returns**, but at least one return is below 5%, classify as **Medium Risk**.  
✔ If **all stock returns are 5% or above**, classify as **Low Risk**.  

### **Implementation Steps:**  
🔹 **Step 1:** Use loops to iterate through the list of stock returns.  
🔹 **Step 2:** Implement `if-elif` conditions to classify the risk.  
🔹 **Step 3:** Write a Python program using **ipywidgets** to allow users to **input stock returns interactively** and receive a risk assessment.

---

     import ipywidgets as widgets
     from IPython.display import display

    def assess_risk(returns):
    risk_level = "Low Risk"

    for return_value in returns:
        if return_value < 0:
            risk_level = "High Risk"
            break
        elif return_value < 5:
            risk_level = "Medium Risk"

    return risk_level


    return_widgets = []
    num_stocks = 3
    for i in range(num_stocks):
    widget = widgets.FloatText(
        description=f"Stock {i+1} Return (%):",
        value=0.0,
        step=0.1,
        style={'description_width': 'initial'}
    )
    return_widgets.append(widget)

    assess_button = widgets.Button(description="Assess Risk")

    output = widgets.Output()

    def on_button_clicked(b):
    with output:
        output.clear_output()
        returns = [widget.value for widget in return_widgets]
        risk = assess_risk(returns)
        print(f"Portfolio Risk: {risk}")


     assess_button.on_click(on_button_clicked)

     display(*return_widgets, assess_button, output)

   ## **🟢 Part 3: Loan Repayment Tracker [4 marks]**  

📌 **Requirement:**  
Customers who receive a loan should be able to track their **loan balance** as they make monthly payments. The system should:  
✔ Start with an **initial loan balance** (e.g., PKR 500,000).  
✔ Deduct a **fixed monthly payment** (e.g., PKR 25,000).  
✔ Continue tracking until **loan balance reaches zero**.  
✔ Display the remaining balance **after each payment**.  

### **Implementation Steps:**  
🔹 **Step 1:** Choose an appropriate loop (`for` or `while`).  
🔹 **Step 2:** Ensure the loop **stops once the loan is fully paid**.  
🔹 **Step 3:** Implement a Python program using **ipywidgets** to **simulate loan repayment interactively**.

---

          import ipywidgets as widgets
            from IPython.display import display

         initial_loan_balance = widgets.FloatText(
             description="Initial Loan Balance (PKR):",
             value=500000.0,
             step=10000.0,
             style={'description_width': 'initial'}
         )

         monthly_payment = widgets.FloatText(
             description="Monthly Payment (PKR):",
             value=25000.0,
             step=1000.0,
             style={'description_width': 'initial'}
         )

         track_button = widgets.Button(description="Track Repayment")

         output = widgets.Output()

         def track_repayment(loan_balance, payment):
             payment_number = 0
             while loan_balance > 0:
                 payment_number += 1
                 loan_balance -= payment
                 if loan_balance < 0:
                     loan_balance = 0
                 print(f"Payment {payment_number}: Remaining Balance: PKR {loan_balance:.2f}")

         def on_track_button_clicked(b):
             with output:
                 output.clear_output()
                 loan_balance = initial_loan_balance.value
                 payment = monthly_payment.value
                 track_repayment(loan_balance, payment)


            track_button.on_click(on_track_button_clicked)

            display(initial_loan_balance, monthly_payment, track_button, output)

            
## **🟢 Part 4: Stock Price Monitoring and Trading Strategy [4 marks]**  

📌 **Requirement:**  
A stock trader wants to **track stock prices daily** and **sell when the price reaches PKR 200**. The system should:  
✔ Iterate through a **list of stock prices**.  
✔ **Skip missing stock data** (`None` values).  
✔ Stop tracking **once the price reaches PKR 200**.  

### **Implementation Steps:**  
🔹 **Step 1:** Handle missing stock data using `continue`.  
🔹 **Step 2:** Stop tracking once the stock hits the target price (`break`).  
🔹 **Step 3:** Write a Python program using **ipywidgets** to **process stock prices interactively** and trigger alerts when conditions are met.

---

            import ipywidgets as widgets
            from IPython.display import display

            # Stock Prices Input
            stock_prices_text = widgets.Textarea(
                value="",
                placeholder="Enter stock prices separated by commas (e.g., 150,160,None,180,200)",
                description="Stock Prices:",
                disabled=False,
                style={'description_width': 'initial'}
            )

            monitor_button = widgets.Button(description="Start Monitoring")

            output = widgets.Output()


            def monitor_stock_prices(prices):
                """Monitors stock prices and triggers an alert when the price reaches 200."""
                for i, price_str in enumerate(prices):
                    if price_str is None or price_str.strip() == "":  # Handle None or empty strings
                        print(f"Skipping day {i+1}: Missing data")
                        continue  # Skip to the next day

                    try:
                        price = float(price_str)
                    except ValueError:
                        print(f"Skipping day {i+1}: Invalid price format '{price_str}'")
                        continue # Skip to the next day if conversion fails

                    print(f"Day {i+1}: Stock Price: PKR {price:.2f}")

                    if price >= 200:
                        print("Alert! Stock price reached PKR 200. Selling now!")
                        break  # Stop monitoring

            def on_monitor_button_clicked(b):
                with output:
                    output.clear_output()
                    prices_str = stock_prices_text.value
                    prices_list = [p.strip() for p in prices_str.split(",")]  # Split and strip whitespace
                    monitor_stock_prices(prices_list)


            monitor_button.on_click(on_monitor_button_clicked)

            display(stock_prices_text, monitor_button, output)

            
## **🟢 Part 5: Currency Exchange Rate Tracker [4 marks]**  

📌 **Requirement:**  
SecureBank provides **real-time currency exchange tracking**. The system should:  
✔ Start at **PKR 290/USD**.  
✔ Increase by **1 PKR per day** until it reaches **PKR 300/USD**.  
✔ Print exchange rates daily and stop when the **target rate is reached**.  

### **Implementation Steps:**  
🔹 **Step 1:** Choose a suitable loop (`for` or `while`).  
🔹 **Step 2:** Stop the loop when the exchange rate reaches the target.  
🔹 **Step 3:** Implement a Python program using **ipywidgets** to **track the currency exchange rate interactively**.

---

         import ipywidgets as widgets
         from IPython.display import display

         # Initial Exchange Rate and Target Rate
         initial_rate = widgets.FloatText(
             description="Initial Exchange Rate (PKR/USD):",
             value=290.0,
             step=0.1,
             style={'description_width': 'initial'}
         )

         target_rate = widgets.FloatText(
             description="Target Exchange Rate (PKR/USD):",
             value=300.0,
             step=0.1,
             style={'description_width': 'initial'}
         )

         track_button = widgets.Button(description="Track Exchange Rate")

         output = widgets.Output()

         def track_exchange_rate(start_rate, target):
             """Tracks the currency exchange rate daily until the target rate is reached."""
             current_rate = start_rate
             day = 0
             while current_rate <= target:
                 day += 1
                 print(f"Day {day}: Exchange Rate: PKR {current_rate:.2f}/USD")
                 if current_rate == target:
                     print("Target exchange rate reached!")
                     break
                 current_rate += 1


         def on_track_button_clicked(b):
             with output:
                 output.clear_output()
                 start_rate = initial_rate.value
                 target = target_rate.value
                 track_exchange_rate(start_rate, target)


         track_button.on_click(on_track_button_clicked)

         display(initial_rate, target_rate, track_button, output)

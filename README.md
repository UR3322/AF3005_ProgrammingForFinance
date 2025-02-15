   📘  **Smart Financial Management System** 

📍**FAST National University of Computer and Emerging Sciences **(FAST-NUCES)**, Islamabad**

👨‍🏫 **Instructor:** **Dr. Usama Arshad (Assistant Professor, FSM)**

🎓 **Program:** **BS Financial Technology** **(BSFT)**

📅 **Semester:** **Spring 2025**


 ## **🟢 Part 1: Loan Eligibility & Interest Rate Calculation**  

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

**1. Input: Collects employment, income, and credit score from the user.**

**2. Employment Check: Immediately rejects the loan if the applicant is unemployed.**

**3. Income Check: Rejects the loan if income is below 50,000 PKR.**

**4. Credit Score Check: Determines interest rate (5% or 8%) based on credit score; rejects the loan if too low.**

**5. Approval/Rejection: Prints "Loan Approved!" with the interest rate or "Loan Rejected!" with the reason.**

**6. Execution: check_loan_eligibility() starts the process.**

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

## **🟢 Part 2: Investment Risk Assessment**  

📌 **Requirement:**  
SecureBank offers **investment analysis services**. The system should evaluate a **portfolio of stocks** and classify the risk level based on stock returns:  
✔ If **any stock has a negative return**, the portfolio is **High Risk**.  
✔ If **all stocks have positive returns**, but at least one return is below 5%, classify as **Medium Risk**.  
✔ If **all stock returns are 5% or above**, classify as **Low Risk**.  

### **Implementation Steps:**  
 **1. Input: Collects stock returns (percentages) from the user via interactive widgets.** 
 
 **2. High Risk Check: If ANY stock has a negative return, the portfolio is classified as "High Risk".** 
 
 **3. Medium Risk Check: If ALL stocks have positive returns, but at least one is below 5%, it's "Medium Risk".** 
 
**4. Low Risk: If ALL stock returns are 5% or higher, it's "Low Risk".** 

**5. Output: Displays the calculated portfolio risk level ("High Risk", "Medium Risk", or "Low Risk").** 

**6. Execution: Interactive widgets and a button are displayed, triggering the assessment upon button click.**


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

   ## **🟢 Part 3: Loan Repayment Tracker**  

📌 **Requirement:**  
Customers who receive a loan should be able to track their **loan balance** as they make monthly payments. The system should:  
✔ Start with an **initial loan balance** (e.g., PKR 500,000).  
✔ Deduct a **fixed monthly payment** (e.g., PKR 25,000).  
✔ Continue tracking until **loan balance reaches zero**.  
✔ Display the remaining balance **after each payment**.  

### **Implementation Steps:**  
 **1. Input: Takes the initial loan balance and monthly payment amount from the user through interactive widgets.**
 
 **2. Repayment Simulation: Simulates monthly loan repayments by deducting the payment from the balance.**
 
 **3. Zero Balance Condition: Stops the simulation when the loan balance reaches zero (or goes negative, then sets to zero).**
 
 **4. Display Balance: Displays the remaining loan balance after each monthly payment.**
 
 **5. Looping: Continues the repayment simulation until the loan is fully paid off.**
 
 **6. Execution: Interactive widgets (initial balance, payment) and a "Track Repayment" button are displayed.  Clicking the button triggers the repayment tracking process.**

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

            
## **🟢 Part 4: Stock Price Monitoring and Trading Strategy**  

📌 **Requirement:**  
A stock trader wants to **track stock prices daily** and **sell when the price reaches PKR 200**. The system should:  
✔ Iterate through a **list of stock prices**.  
✔ **Skip missing stock data** (`None` values).  
✔ Stop tracking **once the price reaches PKR 200**.  

### **Implementation Steps:**  
 **1. Input: Accepts a comma-separated list of daily stock prices from the user via a text area widget.** 

 **2. Data Cleaning: Skips missing stock data (None values or empty strings) and handles invalid price formats.**

 **3. Price Monitoring: Iterates through the cleaned list of stock prices, displaying each day's price.**

 **4. Sell Trigger: Stops monitoring and issues an alert when the stock price reaches or exceeds PKR 200.**

 **5. Iteration Stop: The monitoring process terminates once the sell trigger condition is met.**

 **6. Execution: Displays the text area for input, a "Start Monitoring" button, and an output area. Clicking the button initiates the price monitoring process.**

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

            
## **🟢 Part 5: Currency Exchange Rate Tracker**  

📌 **Requirement:**  
SecureBank provides **real-time currency exchange tracking**. The system should:  
✔ Start at **PKR 290/USD**.  
✔ Increase by **1 PKR per day** until it reaches **PKR 300/USD**.  
✔ Print exchange rates daily and stop when the **target rate is reached**.  

### **Implementation Steps:**  

 **1. Input: Takes the initial and target exchange rates (PKR/USD) from the user through interactive widgets.**
 
 **2. Daily Rate Increment: Simulates the daily increase of the exchange rate by 1 PKR.**
 
 **3. Target Reached Condition: Stops tracking when the exchange rate reaches or exceeds the specified target rate.**
 
 **4. Display Daily Rate: Prints the exchange rate for each day of the simulation.**
 
 **5. Termination Message: Displays a message indicating that the target exchange rate has been reached.**

 **6. Execution: Displays widgets for initial and target rates, a "Track Exchange Rate" button, and an output area. 
  Clicking the button starts the exchange rate tracking process.**

  
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

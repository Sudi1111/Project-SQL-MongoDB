Database Creation Details
MySQL (Structured Data)
1. Customer Table:
- Fields: customer_id (Primary Key), name, age, income, credit_score, address, customer_since.
- File: `customer_table.csv`.
- Purpose: Stores customer demographic and financial details.

2. Loan Table:
- Fields: loan_id (Primary Key), customer_id (Foreign Key), loan_amount, loan_purpose, default_risk.
- File: `loan_table.csv`.
- Purpose: Stores loan details linked to customers.

3. Transaction Table:
- Fields: transaction_id (Primary Key), loan_id (Foreign Key), customer_id (Foreign Key), transaction_amount, transaction_type, transaction_date.
- File: `transaction_table.csv`.
- Purpose: Records loan-related transactions.

MongoDB (Unstructured Data)

1. Behavior Logs Collection:
- Fields: customer_id, timestamp, action, device, ip_address, location.
- File: `shuffled_balanced_behavior_logs.json`.
- Purpose: Tracks customer behavior patterns.

2. Customer Feedback Collection:
- Fields: loan_id, customer_id, feedback_text, sentiment_score, feedback_category, escalation_flag, escalation_reason.
- File: `realistic_customer_feedback.json`.
- Purpose: Stores customer feedback and sentiment analysis.

Tasks with MySQL
1. Customer Risk Analysis: Identify customers with low credit scores and high-risk loans to predict potential defaults and prioritize risk mitigation strategies.
2. Loan Purpose Insights: Determine the most popular loan purposes and their associated revenues to align financial products with customer demands
3. High-Value Transactions: Detect transactions that exceed 30% of their respective loan amounts to flag potential fraudulent activities
4. Missed EMI Count: Analyze the number of missed EMIs per loan to identify loans at risk of default and suggest intervention strategies
5. Regional Loan Distribution: Examine the geographical distribution of loan disbursements to assess regional trends and business opportunities. 
6. Loyal Customers: List customers who have been associated with Cross River Bank for over five years and evaluate their loan activity to design loyalty programs.
7. High-Performing Loans: Identify loans with excellent repayment histories to refine lending policies and highlight successful products.
8. Age-Based Loan Analysis: Analyze loan amounts disbursed to customers of different age groups to design targeted financial products.
9. Seasonal Transaction Trends: Examine transaction patterns over years and months to identify seasonal trends in loan repayments.
10. Fraud Detection: Highlight potential fraud by identifying mismatches between customer address locations and transaction IP locations.
11. Repayment History Analysis: Rank loans by repayment performance using window functions.
12. Credit Score vs. Loan Amount: Compare average loan amounts for different credit score ranges.
13. Top Borrowing Regions: Identify regions with the highest total loan disbursements.
14. Early Repayment Patterns: Detect loans with frequent early repayments and their impact on revenue.
15. Feedback Correlation: Correlate customer feedback sentiment scores with loan statuses.
Tasks with MongoDB
CRUD Operations

1. Insert New Feedback

Input: Adding feedback for a customer and loan, capturing sentiments and details about the loan process.

Sample Input:

{

    "loan_id": 2001,

    "customer_id": 101,

    "feedback_text": "The loan approval process was seamless, but the interest rate was slightly higher than expected.",

    "sentiment_score": 0.7,

    "feedback_category": "Approval Process",

    "escalation_flag": false,

    "escalation_reason": null,

    "timestamp": "2024-11-15T10:30:00Z"

}

Expected Database Entry:

{

    "loan_id": 2001,

    "customer_id": 101,

    "feedback_text": "The loan approval process was seamless, but the interest rate was slightly higher than expected.",

    "sentiment_score": 0.7,

    "feedback_category": "Approval Process",

    "escalation_flag": false,

    "escalation_reason": null,

    "timestamp": "2024-11-15T10:30:00Z"

}


2. Update Escalation Flags

Input: Update escalation flags in feedback to include specific reasons for unresolved customer complaints.

Sample Feedback Before Update:

{

    "loan_id": 2002,

    "customer_id": 102,

    "feedback_text": "Customer service was unresponsive to my queries.",

    "sentiment_score": -0.6,

    "feedback_category": "Customer Service",

    "escalation_flag": true,

    "escalation_reason": null

}

Feedback After Update:

{

    "loan_id": 2002,

    "customer_id": 102,

    "feedback_text": "Customer service was unresponsive to my queries.",

    "sentiment_score": -0.6,

    "feedback_category": "Customer Service",

    "escalation_flag": true,

    "escalation_reason": "Delayed response from customer service"

}


3. Remove Duplicate Behavior Logs

Input: Remove duplicate entries with the same customer_id and timestamp.

Sample Logs Before Removal:

[

    { "customer_id": 103, "timestamp": "2024-11-15T12:00:00Z", "action": "Login", "device": "Mobile" },

    { "customer_id": 103, "timestamp": "2024-11-15T12:00:00Z", "action": "Login", "device": "Mobile" }

]

Logs After Removal:

[

    { "customer_id": 103, "timestamp": "2024-11-15T12:00:00Z", "action": "Login", "device": "Mobile" }

]


4. Retrieve Positive Feedback                                  

Input: Retrieve feedback entries with sentiment scores greater than 0.5.

Sample Output:

[

    {

        "loan_id": 2003,

        "customer_id": 104,

        "feedback_text": "The repayment terms were flexible and suited my needs.",

        "sentiment_score": 0.9

    },

    {

        "loan_id": 2004,

        "customer_id": 105,

        "feedback_text": "Customer service was prompt and helpful during the loan application process.",

        "sentiment_score": 0.8

    }

]


5. Fetch Logs for 'Missed Payment' Actions

Input: Retrieve behavior logs where the action is "Missed Payment."

Sample Output:

[

    {

        "customer_id": 106,

        "timestamp": "2024-10-10T08:45:00Z",

        "device": "Desktop",

        "ip_address": "192.168.1.101"

    },

    {

        "customer_id": 107,

        "timestamp": "2024-10-12T14:00:00Z",

        "device": "Mobile",

        "ip_address": "10.0.0.45"

    }

]

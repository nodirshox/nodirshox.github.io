---
layout: post
title: "Mastering transactional database queries: Leveraging Prisma for accurate data"
categories: ["tutorial", "nodejs"]
permalink: /transactional-query
---

![Prisma.io](/assets/2024-02-25-transactional-query/poster.png)

In a recent side project, I encountered the challenge of importing CSV data into a PostgreSQL database. For this task, I utilized [Prisma](https://prisma.io){:target="_blank"}, an ORM (Object Relational Mapping) tool, to facilitate database queries. The CSV data, comprising 1,000 rows, detailed financial transactions categorized as either EXPENSE or INCOME.

A critical requirement was the precise calculation and update of the wallet's balance with each transaction. Consider this example:

**Initial Wallet Balance**: 0

Sample Transactions

```
[
  {
    amount: 100
    type: INCOME
  },
  {
    amount: 50
    type: EXPENSE
  },
  {
    amount: 25
    type: EXPENSE
  }
]

```

**Expected Final Wallet Balance**: 75

To implement this functionality, I developed a function to insert individual transactions into the database and update the wallet balance accordingly:

```
async createTransaction(
  walletId: string,
  transactionAmount: number,
  transactionType: TransactionType,
) {
  const wallet = await this.prisma.wallet.findUnique({where: { id: walletId }})

  const updateWallet = this.prisma.wallet.update({
    where: { id: walletId },
    data: {
      amount: this.utils.calculateFinalWalletAmount(wallet.amount, transactionAmount, transactionType),
    },
  })

  const transaction = this.prisma.transaction.create({
    data: {
      amount: transactionAmount,
      type: transactionType,
    }
  })

  const result = await this.prisma.$transaction([updateWallet, transaction])

  return result
}
```

This approach directly modifies the wallet amount using the helper function **calculateFinalWalletAmount**, which adjusts the balance based on the transaction type (adding for INCOME and subtracting for EXPENSE).

While this method worked well for a small number of transactions, issues arose when I parsed and inserted 1,000 rows from the CSV into the database. Due to the high rate of function calls (over 100 per second or maybe more), concurrent executions sometimes failed to accurately capture the wallet's latest state, leading to incorrect final balances.

## Refactoring for Accuracy

To address this concurrency issue, I refactored the createTransaction function:

```
async createTransaction(
  walletId: string,
  transactionAmount: number,
  transactionType: TransactionType,
) {
  const updateWallet = this.prisma.wallet.update({
    where: { id: walletId },
    data: {
      amount: {
        increment: this.utils.setTransactionA(type, transactionAmount),
      },
    },
  })

  const transaction = this.prisma.transaction.create({
    data: {
      amount: transactionAmount,
      type: transactionType,
    }
  })

  const result = await this.prisma.$transaction([updateWallet, transaction])

  return result
}
```

The key change involves the new helper function **setTransactionAmount**, which determines the sign of the transaction amount (positive for INCOME, negative for EXPENSE) and utilizes Prisma's increment method to adjust the wallet balance. This method ensures atomicity and consistency of the wallet amount, even under high concurrency.

After applying this refactor, processing the same 1,000 transactions resulted in accurate calculation of the final wallet balance.

## Conclusion

This experience underscores the importance of considering concurrency and the state management of database operations, especially when dealing with financial transactions. By adjusting our approach to transaction insertion and balance calculation, we can ensure accuracy and reliability in real-time financial applications.

P.S: ChatGPT is used to make article more clear for reading.

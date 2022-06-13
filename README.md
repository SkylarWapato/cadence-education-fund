

# Cadence education fund
First a few ground rules.
> :warning: **Expected error**: This will denote an error that is expected to occur (a good error).

> ℹ️ **Info**: General helpful information

## Deploy FLOW contracts

Deploy the FungibleToken interface on 0x01

Deploy the FlowToken contract on 0x02

![Flow Contracts](assets/flow-contracts.png)

## Deploy fund contracts

Deploy the FundChild interface on 0x03

Deploy the EducationFund contract on 0x04

![Fund Contracts](assets/fund-contracts.png)

## Get FLOW ready for use
> ℹ️ **Info**: In the interest of demo time this transaction will set up FLOW for all accounts at once.  This call will set up basic flow vaults/storage/references

Call "Set up FLOW" transaction signed by all accounts.

![All Accounts](assets/all-accounts.png)

You should see the following output:

![Set up FLOW](assets/set-up-flow.png)

## Check FLOW balances

Execute the "Check FLOW balances" script

You should see the following output:

![Check balances](assets/check-flow-zero.png)

## Mint FLOW for all accounts
> ℹ️ **Info**: We use this account because it is the owner of the FlowToken contract

Call "Mint FLOW for all accounts" transaction signed by account 0x02

![Mint FLOW signer](assets/mint-flow.png)

You should see the following output:

![Minted FLOW](assets/mint-flow-results.png)

## Check the account balances again

Execute the "Check FLOW balances" script

You should see the following output:

> ℹ️ **Info**: As you can see, 1000 FLOW was minted and 200 FLOW was given to each account

![Check balances](assets/check-flow.png)

## Start the fund
> ℹ️ **Info**: We will use accounts 0x01 (Manager) and 0x05 (Beneficiary) but this could be done with any two accounts

Call "Start fund" transaction signed by 0x01 (Manager) and 0x05 (Beneficiary) in that order

![Start fund signers](assets/start-fund-signers.png)

You should see the following output:

![Fund established](assets/fund-established.png)

## Check the fund's balance

Execute "Check fund balance" script

You should see the following output:

![Check fund balance](assets/fund-balance-zero.png)

## Make your first donation to the fund

Let's make a 50 FLOW donation with account 0x03 (just because 0x03 is unaffiliated with the fund)

Call "Public donation (50)" transaction signed by account 0x03

You should see the following output:

![Donation success](assets/donation-success.png)

## Check the account balances again

Execute the "Check FLOW balances" script

You should see the following output:

> ℹ️ **Info**: 50 FLOW moved from account 0x03 to the fund!

![Check balances](assets/balances-post-1st-don.png)

## Check the fund's balance again

Execute "Check fund balance" script

You should see the following output:

> ℹ️ **Info**: We have FLOW in our fund!

![Check fund balance](assets/fund-balance-post-1st.png)

## As fund benificiary, try to withdraw 50 FLOW (a pre condition failure is expected)
> ℹ️ **Info**: Accounts 0x01 and 0x05 will be refered to as 0x01 (Manager) and 0x05 (Beneficiary), respectively

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

Should FAIL with the following output:

![Non-grad fail](assets/non-grad-fail.png)

> ℹ️ **Info**: This failure was expected as the Manager's condition of first graduating post-secondary school hadn't been met

## As fund manager, mark the beneficiary as graduated

Call "Set graduated" transaction signed by account 0x01 (Manager)

![Set grad signer](assets/set-grad-signer.png)

You should see the following output:

![Grad success](assets/set-grad-success.png)

## As fund benificiary, try to withdraw 50 FLOW (this too will fail because the limit defaults to zero!)

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

Should FAIL with the following output:

![Limit fail](assets/limit-fail-1st.png)

> ℹ️ **Info**: This failure was expected as the Manager's condition of first graduating post-secondary school hadn't been met

## As fund manager, set the beneficiary's limit to 100 FLOW

Call "Set limit (100)" transaction signed by account 0x01 (Manager)

![Set limit signer](assets/set-grad-signer.png)

You should see the following output:

![Limit success](assets/set-limit-success-1st.png)

## As fund benificiary, withdraw 50 FLOW (we can finally do it!)

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

You should see the following output:

![Withdraw success](assets/withdraw-success-1st.png)

> ℹ️ **Info**: Feel free to check the account or fund balances by executing "Check FLOW balances" and "Check fund balance" scripts respectively

## Somebody is donating 100 FLOW!

Let's make two 50 FLOW donations with account 0x04

> ℹ️ **Info**: Call this transaction twice, that's what the (x2) is signifying

Call "Public donation (50)" transaction signed by account 0x04 (x2)

You should see the following output:

![Donation success](assets/100-flow-don.png)


## As fund benificiary, withdraw 50 FLOW

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

You should see the following output:

![Withdraw success](assets/withdraw-success-1st.png)

> ℹ️ **Info**: Feel free to check the account or fund balances by executing "Check FLOW balances" and "Check fund balance" scripts respectively


## As fund benificiary, withdraw 50 more FLOW (this will fail because we have reached our limit)

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

Should FAIL with the following output:

![Withdraw failure](assets/limit-fail-2nd.png)

## As fund manager, set the beneficiary's limit back to 100 FLOW

Call "Set limit (100)" transaction signed by account 0x01 (Manager)

![Set limit signer](assets/set-grad-signer.png)

You should see the following output:

![Limit success](assets/set-limit-success-1st.png)

## Now the withdrawal will succeed!

Call "Fund withdraw (50)" transaction signed by 0x05 (Beneficiary)

![Withdraw signer](assets/withdraw-fail-1st-signer.png)

You should see the following output:

![Withdraw success](assets/withdraw-success-1st.png)

## Confirm the balances

Execute the "Check FLOW balances" script

You should see the following output:

> ℹ️ **Info**: We should see 50 FLOW missing from account 0x03 and 100 FLOW from account 0x04.  The 150 FLOW hs gone to the fund and the withdrawn by 0x05 (Beneficiary)

![Check balances](assets/final-account-balances.png)

## Manager should not be able to reduce limit

### Set limit to 100

Call "Set limit (100)" transaction signed by account 0x01 (Manager)

![Set limit signer](assets/set-grad-signer.png)

You should see the following output:

![Limit success](assets/set-limit-success-1st.png)

### Try to do a lower limit

On "Set limit (100)", Change line 7 to 99.0

![Code change](assets/code-change.png)

Call "Set limit (100)" transaction signed by account 0x01 (Manager)

![Set limit signer](assets/set-grad-signer.png)

Should FAIL with the following output:

![Limit fail](assets/limit-decrease-fail.png)

> ℹ️ **Info**: Please set line 7 back to 100

# Thank you very much!